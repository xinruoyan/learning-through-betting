Goose Fighting Monsters

```
import sys
from time import sleep


import pygame

from settings import Settings
from game_stats import GameStats
from scoreboard import Scoreboard
from button import Button
from ship import Ship
from bullet import Bullet
from alien import Alien

class AlienInvasion:
    #overall class to manage game assets and behavior.
    def __init__(self):
        #initialize the game, and creat game resources.
        pygame.init()
        self.clock = pygame.time.Clock()
        self.settings = Settings()

        self.screen = pygame.display.set_mode((self.settings.screen_width,self.settings.screen_height))
        pygame.display.set_caption("Fighting Goose")

        #creat an instance to store game statistics.
        # and creat a scoreboard.
        self.stats = GameStats(self)
        self.sb = Scoreboard(self)
        self.ship = Ship(self)
        self.bullets = pygame.sprite.Group()
        self.aliens = pygame.sprite.Group()
        self._creat_fleet()

        #set the background color.
        self.bg_color = self.settings.bg_color
        #start alien invasion in an active state.
        self.game_active = False
        #make the play button.
        self.play_button = Button(self,"START")

    def run_game(self):
        #start the main loop for the game.
        while True:
            self._check_events()
            self._update_screen()

            if self.game_active:
                self.ship.update()
                self._update_bullets()     
                self._update_aliens()      
                # print(len(self.bullets))
                
                self.clock.tick(60)

    def _update_screen(self):
            #redraw the screen during each pass through the loop.
            #update images on the screen, and flip to the new screen.
            self.screen.fill(self.settings.bg_color)
            for bullet in self.bullets.sprites():
                bullet.draw_bullet()
            self.ship.blitme()
            self.aliens.draw(self.screen)
            #draw the score information.
            self.sb.show_score()
            #draw the play button if the game is inactive.
            if not self.game_active:
                self.play_button.draw_button()
            #make the most recently drawn screen visible.
            pygame.display.flip()

    def _check_aliens_left(self):
        #check if any aliens have reached the left of the screen.
        for alien in self.aliens.sprites():
            if alien.rect.left <= 0:
                #treat this the same as if the ship got hit.
                self._ship_hit()
            break

    def _creat_fleet(self):
        #creat the fleet of aliens.
        #make an alien.
        alien = Alien(self)
        #set the alien's initial position to the top-right corner.
        alien_width = alien.rect.width
        alien_height = alien.rect.height
        available_space_y = self.settings.screen_height - (2*alien_height)
        number_aliens_y = available_space_y //(alien_height)
        #calculate the number of aliens that can fit in a row
        available_space_x = self.settings.screen_width - (2*alien_width)
        number_aliens_x = available_space_x // (2*alien_width)

        #creat the fleet of aliens
        
        for alien_number_y in range(number_aliens_y):
            for alien_number_x in range(number_aliens_x):
                alien = Alien(self)
                alien.x = 250+2*alien_width + 2*alien_number_x * alien_width
                alien.y = 10 + 1.2*alien_number_y * alien_height
                alien.rect.x = alien.x
                alien.rect.y = alien.y
                self.aliens.add(alien)

        self.aliens.add(alien)

    def _check_fleet_edges(self):
        #respond appropriately if any aliens have reached an edge.
        for alien in self.aliens.sprites():
            if alien.check_edges():
                self._change_fleet_direction()
                break
    def _change_fleet_direction(self): 
        #drop the entire fleet and change the fleet's direction.
        for alien in self.aliens.sprites():
            alien.rect.x -= self.settings.fleet_drop_speed 
        self.settings.fleet_direction *= -1

    def _update_bullets(self):
        #update bullet positions.
        self.bullets.update()
        #get rid of bullets that have disappeared.
        for bullet in self.bullets.copy():
            if bullet.rect.right > 1300:
                self.bullets.remove(bullet)
        self._check_bullet_alien_collisions()

    def _check_bullet_alien_collisions(self):

        collisions = pygame.sprite.groupcollide(
            self.bullets, self.aliens, True, True
        )
        if collisions:
            for aliens in collisions.values():
                self.stats.score += self.settings.alien_points * len(aliens)
                self.sb.prep_score()
                self.sb.check_high_score()
        if not self.aliens:
            #destroy existing bullets and creat new fleet.
            self.bullets.empty()
            self._creat_fleet()
            self.settings.increase_speed()
            #increase level.
            self.stats.level += 1
            self.sb.prep_level()


    def _update_aliens(self):
        #update the positions of all aliens in the fleet.
        #check if the fleet is at an edge, then update positions.
        self._check_fleet_edges()
        self.aliens.update()
        #look for alien-ship collisions.
        if pygame.sprite.spritecollideany(self.ship, self.aliens):
            self._ship_hit()
        
        self._check_aliens_left()


    def _check_events(self):
        #respond to keypresses and mouse events.
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                sys.exit()
            elif event.type == pygame.KEYDOWN:
                self._check_keydown_events(event)
                     
            elif event.type == pygame.KEYUP:
                self._check_keyup_events(event)      

            elif event.type == pygame.MOUSEBUTTONDOWN:
                mouse_pos = pygame.mouse.get_pos()
                self._check_play_button(mouse_pos)              
                                                    
                          #move the ship to the right.
                            #   self.ship.rect.x += 1
    def _check_play_button(self, mouse_pos):
        #start a new game when the player clicks play.
        button_clicked = self.play_button.rect.collidepoint(mouse_pos)
        if button_clicked and not self.game_active:
            #reset the game statistics.
            self.settings.initialize_dynamic_settings()
            self.stats.reset_stats()
            self.sb.prep_score()
            self.sb.prep_level()
            self.sb.prep_ships()
            self.game_active = True
            #get rid of any remaining bullets and aliens.
            self.bullets.empty()
            self.aliens.empty()
            #creat a new fleet and center the ship.
            self._creat_fleet()
            self.ship.center_ship()
            #hide the mouse cursor.
            pygame.mouse.set_visible(False)

    def _check_keydown_events(self,event):
         #respond to keypresses.
         if event.key == pygame.K_UP:              
            self.ship.moving_up = True
         elif event.key == pygame.K_DOWN:
            self.ship.moving_down = True
         elif event.key == pygame.K_RIGHT:
            self.ship.moving_right = True
         elif event.key == pygame.K_LEFT:
            self.ship.moving_left = True    
         elif event.key == pygame.K_q:
            sys.exit()
         elif event.key == pygame.K_SPACE:
            self._fire_bullet()
    def _check_keyup_events(self,event):
         #respond to key releases.
         if event.key == pygame.K_UP:
            self.ship.moving_up = False
         elif event.key == pygame.K_DOWN:
            self.ship.moving_down = False
         elif event.key == pygame.K_RIGHT:
            self.ship.moving_right = False
         elif event.key == pygame.K_LEFT:
            self.ship.moving_left = False
    def _fire_bullet(self):
        #creat a new bullet and add it to the bullets group.
        if len(self.bullets) < self.settings.bullets_allowed:
             new_bullet = Bullet(self)
             self.bullets.add(new_bullet)

    def _ship_hit(self):
        #respond to the ship being hit by an alien.
        #decrement ship_left.
        if self.stats.ships_left > 0:
            self.stats.ships_left -= 1
            self.sb.prep_ships()
            #get rid of any remaining bullets and aliens.
            self.bullets.empty()
            self.aliens.empty()
            #creat a new fleet and center the ship.
            self._creat_fleet()
            self.ship.center_ship()
            #pause.
            sleep(0.5)
        else:
            self.game_active = False
            pygame.mouse.set_visible(True)

 
if __name__ == '__main__':
    #make a game instance, and run the game.
    ai = AlienInvasion()
    ai.run_game()
```


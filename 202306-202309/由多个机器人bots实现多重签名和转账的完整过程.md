##                     多个机器人bots实现多重签名和转账的完整过程

- [ ] by ：dada  2023.07.26

#### 一、基本概念：

1、多签钱包：由多个接收者地址（> =2）共同组成的账户，并且定义了多重签名者数量（threshold >=1），该账户即为多重签名钱包。

2、多重签名者阀值（threshold）：threshold 值范围(1=< N <= 多签钱包接收者地址数量)。

3、多重签名：简称：多签，实现从多签钱包转出一定数量的资产，需要达到多签阀值（threshold）要求；签名者可以是bot，也可以是普通的user，具体视多签钱包成员的“user_id”组成情况。

 如:3/4 表示该多签钱包有4位接收者；实现转账的多签数为：3；即，至少3名钱包内的成员成功签名，才能完成从钱包实现资产转移。 

4、转账发起和撤销：多签钱包内的任何一名成员都可以发起多签转账；但要实现转账必须满足最少签名者（含发起者）的成功签名配合；在未获得足够数量的多签前，任意一名成员可以撤销该发起的转账申请。

#### 二、转账过程：

 第一步：往多签钱包内转账；

 第二步：核查多签钱包内的资产状况， 获取 utxo；即：钱包内有state  === "unspent" UTXO （Unspent Transaction Output）

第三步： 构建多签交易 raw（未签名的原始交易数据）

第四步：通过 raw 构建签名交易请求

第五步：对需要签名的交易进行签名

第六步：将签名完成的交易发送给主网（mixin）

第七步：查询utxo消息，获取 状态为 "spent" ，以及 transaction_hash 值与”unspent“ utxo 消息中的相同 。

交易完成。此时收款人钱包里的对应资产记录里，会多一条多签的转账记录。

#### 三、多签实现案例各步骤及消息解读

1. ##### 转账发起和首签

###### 第一步：省略

###### **第二步：核查多签钱包内的资产状况， 获取多签 utxo**

   **执行**：client.readMultisigOutputs(members， threshold）

 **输出：**

  { 
  type: 'multisig_utxo',   //消息类型 多签 utxo
  user_id: '9baed511-faf9-47dc-b6ce-6abe3dfbe5ab',   //查询发起者
  utxo_id: '216c0606-84eb-38e3-ad32-adbfb8f68ebd',
  asset_id: '4d8c508b-91c5-375b-92b0-ee702ed2dac5', // 资产类型 ：**USDT**
  transaction_hash: 'd6d3851b9c91172d72a3d948f358b89d8f662e058091dd61e943f39a555e7516',
  output_index: 1,
  amount: '0.49415',  // **资产数量**
  threshold: 3,  //**阈值：3，即：至少3名成员签名**

  members: [  // **多签钱包含四名成员,dada 和 3名bot**
    '30ec2dc7-76aa-4c3a-83c4-114bbbf3183b',
    '57915058-dc64-4973-a7ad-5372c0a88879',
    '9baed511-faf9-47dc-b6ce-6abe3dfbe5ab',
    '9dcd64cf-d753-4c53-87d0-bc011fd94cb3'
  ],
  memo: 'Z',
  **state: 'unspent',** // 未花销状态
  sender: '',
  created_at: '2023-07-17T14:47:51.002593Z',
  updated_at: '2023-07-17T14:47:51.002593Z',
  signed_by: '',
  signed_tx: ''
}

###### **第三步：构建多签交易 raw（未签名的原始交易数据）**

将第二步获得的utxo消息，与输出接收者、资产类别和数量，构建多签交易raw：

**执行**： client.makeMultisignTransaction({input:[{
  type: 'multisig_utxo',
  user_id: '9baed511-faf9-47dc-b6ce-6abe3dfbe5ab',
  utxo_id: '216c0606-84eb-38e3-ad32-adbfb8f68ebd',
  asset_id: '4d8c508b-91c5-375b-92b0-ee702ed2dac5',
  transaction_hash: 'd6d3851b9c91172d72a3d948f358b89d8f662e058091dd61e943f39a555e7516',
  output_index: 1,
  amount: '0.49415',
  threshold: 3,
  members: [
    '30ec2dc7-76aa-4c3a-83c4-114bbbf3183b',
    '57915058-dc64-4973-a7ad-5372c0a88879',
    '9baed511-faf9-47dc-b6ce-6abe3dfbe5ab',
    '9dcd64cf-d753-4c53-87d0-bc011fd94cb3'
  ],
  memo: 'Z',
  state: 'unspent',
  sender: '',
  created_at: '2023-07-17T14:47:51.002593Z',
  updated_at: '2023-07-17T14:47:51.002593Z',
  signed_by: '',
  signed_tx: ''
}],
  outputs: [
    {
   receivers: [ '9dcd64cf-d753-4c53-87d0-bc011fd94cb3' ],//**接收者： dada** 
   amount: '0.00015', //转账数量（注：要求<= unspent amount  '0.49415', ）
  threshold: 3,
    },
  ],
  hint: client.newUUID(),
});

**输出**：（raw）

“77770002d4c304ffc3270ee0f3468913bd8027225201f0eccd336d47062d76c6e2b6bb270001d6d3851b9c91172d72a3d948f358b89d8f662e058091dd61e943f39a555e751600010000000000000002000000023a980001f06cce4bb704167f09d05b10df0f739b0bae2959f52859b46d63409f526004d8b7df8ad0338b9dea048de50c0bf2bd57f09142ce18035ec8354385dc1e21175d0003fffe0100000000000402f1c8c00004634fe1c7600a34b399e06f8101d07c66a5b23d0eee4bbf889b9cf2ea4d117cfba8893e5ec2c817055c3a3e9b9445746ee4b9290978d40463edd43a0e6b0b8ec0e575164e6b53c90198a088be4d893f1f2f2f0087d833275afe772dac28563ce74163e7ce8064ec55ad71d975e3f7ef6985a9f9988ea2e11c47060e8d5b889523fe236a0ca2efbd0dd33e6b9606eb69738d27a51667617f7c7da8c35ccc54fde70003fffe03000000015a0000”

###### 第四步：通过 raw 构建签名交易请求

**执行**：client.createMultisig( ’sign‘, raw);

**输出：**

 {
  type: 'multisig_request', //**发起申请消息**
  request_id: '757175cb-a742-4036-bb24-2d0ffb7ca8ea',
  user_id: '9baed511-faf9-47dc-b6ce-6abe3dfbe5ab',
  asset_id: '4d8c508b-91c5-375b-92b0-ee702ed2dac5',
  amount: '0.00015',
  threshold: 3,
  senders: [
    '30ec2dc7-76aa-4c3a-83c4-114bbbf3183b',
    '57915058-dc64-4973-a7ad-5372c0a88879',
    '9baed511-faf9-47dc-b6ce-6abe3dfbe5ab',
    '9dcd64cf-d753-4c53-87d0-bc011fd94cb3'
  ],
  receivers: [ '9dcd64cf-d753-4c53-87d0-bc011fd94cb3' ], //**接收者： dada** 
  signers: [],
  memo: 'Z',
  action: 'sign', 
  state: 'initial',  // **构建签名**
  transaction_hash: '853285a27df68278f0b69417d26507f5f6f3bc12cc1f9e3001b71648e37142b8',
  raw_transaction:  

'77770002d4c304ffc3270ee0f3468913bd8027225201f0eccd336d47062d76c6e2b6bb270001d6d3851b9c91172d72a3d948f358b89d8f662e058091dd61e943f39a555e751600010000000000000002000000023a980001f06cce4bb704167f09d05b10df0f739b0bae2959f52859b46d63409f526004d8b7df8ad0338b9dea048de50c0bf2bd57f09142ce18035ec8354385dc1e21175d0003fffe0100000000000402f1c8c00004634fe1c7600a34b399e06f8101d07c66a5b23d0eee4bbf889b9cf2ea4d117cfba8893e5ec2c817055c3a3e9b9445746ee4b9290978d40463edd43a0e6b0b8ec0e575164e6b53c90198a088be4d893f1f2f2f0087d833275afe772dac28563ce74163e7ce8064ec55ad71d975e3f7ef6985a9f9988ea2e11c47060e8d5b889523fe236a0ca2efbd0dd33e6b9606eb69738d27a51667617f7c7da8c35ccc54fde70003fffe03000000015a0000',  
  created_at: '1970-01-01T00:03:39+00:03',
  code_id: '82db3470-d643-46b6-8537-91ecd2d28a2d'
}

###### 第五步：签名

 **执行：**client.signMultisig( request_id: '757175cb-a742-4036-bb24-2d0ffb7ca8ea',);

 **输出：**

 {
  type: 'multisig_request',
  request_id: '757175cb-a742-4036-bb24-2d0ffb7ca8ea',
  user_id: '9baed511-faf9-47dc-b6ce-6abe3dfbe5ab',
  asset_id: '4d8c508b-91c5-375b-92b0-ee702ed2dac5', // 转账资产类型
  amount: '0.00015', // 转账数量
  threshold: 3,
  senders: [
    '30ec2dc7-76aa-4c3a-83c4-114bbbf3183b',
    '57915058-dc64-4973-a7ad-5372c0a88879',
    '9baed511-faf9-47dc-b6ce-6abe3dfbe5ab',
    '9dcd64cf-d753-4c53-87d0-bc011fd94cb3'
  ],
  receivers: [ '9dcd64cf-d753-4c53-87d0-bc011fd94cb3' ], // **转账接收者**
  signers: [ '9baed511-faf9-47dc-b6ce-6abe3dfbe5ab' ], // **第一个签名者**（转账助手）
  memo: 'Z',
  action: 'sign',
  state: 'signed',
  transaction_hash: '853285a27df68278f0b69417d26507f5f6f3bc12cc1f9e3001b71648e37142b8',
  raw_transaction: '77770002d4c304ffc3270ee0f3468913bd8027225201f0eccd336d47062d76c6e2b6bb270001d6d3851b9c91172d72a3d948f358b89d8f662e058091dd61e943f39a555e751600010000000000000002000000023a980001f06cce4bb704167f09d05b10df0f739b0bae2959f52859b46d63409f526004d8b7df8ad0338b9dea048de50c0bf2bd57f09142ce18035ec8354385dc1e21175d0003fffe0100000000000402f1c8c00004634fe1c7600a34b399e06f8101d07c66a5b23d0eee4bbf889b9cf2ea4d117cfba8893e5ec2c817055c3a3e9b9445746ee4b9290978d40463edd43a0e6b0b8ec0e575164e6b53c90198a088be4d893f1f2f2f0087d833275afe772dac28563ce74163e7ce8064ec55ad71d975e3f7ef6985a9f9988ea2e11c47060e8d5b889523fe236a0ca2efbd0dd33e6b9606eb69738d27a51667617f7c7da8c35ccc54fde70003fffe03000000015a0000',
  created_at: '2023-07-18T04:02:15.990932Z',
  code_id: '82db3470-d643-46b6-8537-91ecd2d28a2d'
}

 *首签完成，等待其他多签和转账...*

2. ##### 第二签 

执行多签第二步，获取utxo 消息（state === “signed”）

 {
  type: 'multisig_utxo',
  user_id: '30ec2dc7-76aa-4c3a-83c4-114bbbf3183b',
  utxo_id: '216c0606-84eb-38e3-ad32-adbfb8f68ebd',
  asset_id: '4d8c508b-91c5-375b-92b0-ee702ed2dac5',
  transaction_hash: 'd6d3851b9c91172d72a3d948f358b89d8f662e058091dd61e943f39a555e7516',
  output_index: 1,
  amount: '0.49415',
  threshold: 3,
  members: [
    '30ec2dc7-76aa-4c3a-83c4-114bbbf3183b',
    '57915058-dc64-4973-a7ad-5372c0a88879',
    '9baed511-faf9-47dc-b6ce-6abe3dfbe5ab',
    '9dcd64cf-d753-4c53-87d0-bc011fd94cb3'
  ],
  memo: 'Z',
  **state: 'signed',** **//获取“signed” 消息**
  sender: '',
  created_at: '2023-07-17T14:47:51.002593Z',
  updated_at: '2023-07-18T04:02:16.713404Z',
  signed_by: '853285a27df68278f0b69417d26507f5f6f3bc12cc1f9e3001b71648e37142b8',
  signed_tx: '77770002d4c304ffc3270ee0f3468913bd8027225201f0eccd336d47062d76c6e2b6bb270001d6d3851b9c91172d72a3d948f358b89d8f662e058091dd61e943f39a555e751600010000000000000002000000023a980001f06cce4bb704167f09d05b10df0f739b0bae2959f52859b46d63409f526004d8b7df8ad0338b9dea048de50c0bf2bd57f09142ce18035ec8354385dc1e21175d0003fffe0100000000000402f1c8c00004634fe1c7600a34b399e06f8101d07c66a5b23d0eee4bbf889b9cf2ea4d117cfba8893e5ec2c817055c3a3e9b9445746ee4b9290978d40463edd43a0e6b0b8ec0e575164e6b53c90198a088be4d893f1f2f2f0087d833275afe772dac28563ce74163e7ce8064ec55ad71d975e3f7ef6985a9f9988ea2e11c47060e8d5b889523fe236a0ca2efbd0dd33e6b9606eb69738d27a51667617f7c7da8c35ccc54fde70003fffe03000000015a0000'
}

**跳过第三步，带入第二步获得的 ” signed_tx“字符串，执行多签第四步，构建交易签名：**

**执行结果：**{
  type: 'multisig_request',
  request_id: '9cd6a576-36a1-40c8-bbbe-2f848d4de0bd',
  user_id: '30ec2dc7-76aa-4c3a-83c4-114bbbf3183b',
  asset_id: '4d8c508b-91c5-375b-92b0-ee702ed2dac5',
  amount: '0.00015',
  threshold: 3,
  senders: [
    '30ec2dc7-76aa-4c3a-83c4-114bbbf3183b',
    '57915058-dc64-4973-a7ad-5372c0a88879',
    '9baed511-faf9-47dc-b6ce-6abe3dfbe5ab',
    '9dcd64cf-d753-4c53-87d0-bc011fd94cb3'
  ],
  receivers: [ '9dcd64cf-d753-4c53-87d0-bc011fd94cb3' ],
  signers: [ '9baed511-faf9-47dc-b6ce-6abe3dfbe5ab' ],
  memo: 'Z',
  action: 'sign',
  **state: 'initial', // 构建交易签名**
  transaction_hash: '853285a27df68278f0b69417d26507f5f6f3bc12cc1f9e3001b71648e37142b8',
  raw_transaction: '77770002d4c304ffc3270ee0f3468913bd8027225201f0eccd336d47062d76c6e2b6bb270001d6d3851b9c91172d72a3d948f358b89d8f662e058091dd61e943f39a555e751600010000000000000002000000023a980001f06cce4bb704167f09d05b10df0f739b0bae2959f52859b46d63409f526004d8b7df8ad0338b9dea048de50c0bf2bd57f09142ce18035ec8354385dc1e21175d0003fffe0100000000000402f1c8c00004634fe1c7600a34b399e06f8101d07c66a5b23d0eee4bbf889b9cf2ea4d117cfba8893e5ec2c817055c3a3e9b9445746ee4b9290978d40463edd43a0e6b0b8ec0e575164e6b53c90198a088be4d893f1f2f2f0087d833275afe772dac28563ce74163e7ce8064ec55ad71d975e3f7ef6985a9f9988ea2e11c47060e8d5b889523fe236a0ca2efbd0dd33e6b9606eb69738d27a51667617f7c7da8c35ccc54fde70003fffe03000000015a0000',
  created_at: '1970-01-01T00:03:39+00:03',
  code_id: 'ca5775a8-0c61-4a18-8f21-dff40804567d'
}

**执行多签第五步（指令同首签），完成第二签**

执行结果：

 {
  type: 'multisig_request',
  request_id: '9cd6a576-36a1-40c8-bbbe-2f848d4de0bd',
  user_id: '30ec2dc7-76aa-4c3a-83c4-114bbbf3183b',
  asset_id: '4d8c508b-91c5-375b-92b0-ee702ed2dac5',
  amount: '0.00015',
  threshold: 3,
  senders: [
    '30ec2dc7-76aa-4c3a-83c4-114bbbf3183b',
    '57915058-dc64-4973-a7ad-5372c0a88879',
    '9baed511-faf9-47dc-b6ce-6abe3dfbe5ab',
    '9dcd64cf-d753-4c53-87d0-bc011fd94cb3'
  ],
  receivers: [ '9dcd64cf-d753-4c53-87d0-bc011fd94cb3' ],
  signers: [
    '9baed511-faf9-47dc-b6ce-6abe3dfbe5ab', // **首签**
    '30ec2dc7-76aa-4c3a-83c4-114bbbf3183b' // **二签**
  ],
  memo: 'Z',
  action: 'sign',
  **state: 'signed',**
  transaction_hash: '853285a27df68278f0b69417d26507f5f6f3bc12cc1f9e3001b71648e37142b8',
  raw_transaction: '77770002d4c304ffc3270ee0f3468913bd8027225201f0eccd336d47062d76c6e2b6bb270001d6d3851b9c91172d72a3d948f358b89d8f662e058091dd61e943f39a555e751600010000000000000002000000023a980001f06cce4bb704167f09d05b10df0f739b0bae2959f52859b46d63409f526004d8b7df8ad0338b9dea048de50c0bf2bd57f09142ce18035ec8354385dc1e21175d0003fffe0100000000000402f1c8c00004634fe1c7600a34b399e06f8101d07c66a5b23d0eee4bbf889b9cf2ea4d117cfba8893e5ec2c817055c3a3e9b9445746ee4b9290978d40463edd43a0e6b0b8ec0e575164e6b53c90198a088be4d893f1f2f2f0087d833275afe772dac28563ce74163e7ce8064ec55ad71d975e3f7ef6985a9f9988ea2e11c47060e8d5b889523fe236a0ca2efbd0dd33e6b9606eb69738d27a51667617f7c7da8c35ccc54fde70003fffe03000000015a0000',
  created_at: '2023-07-18T04:02:21.141114Z',
  code_id: 'ca5775a8-0c61-4a18-8f21-dff40804567d'
}

***二签完成，等待三签.....***

2. ##### 第三签

第三签与第二签前三步骤是一致的；

即，首先读取状态 state===”signed“的utxo，得到 ” signed_tx“字符串，带入执行多签第四步执行，构建交易签名；代人第四步结果中的require_id ,执行第五步，完成签名；结果如下：

**第二步执行结果：**

 {
  type: 'multisig_utxo',
  user_id: '57915058-dc64-4973-a7ad-5372c0a88879',
  utxo_id: '216c0606-84eb-38e3-ad32-adbfb8f68ebd',
  asset_id: '4d8c508b-91c5-375b-92b0-ee702ed2dac5',
  transaction_hash: 'd6d3851b9c91172d72a3d948f358b89d8f662e058091dd61e943f39a555e7516',
  output_index: 1,
  amount: '0.49415',
  threshold: 3,
  members: [
    '30ec2dc7-76aa-4c3a-83c4-114bbbf3183b',
    '57915058-dc64-4973-a7ad-5372c0a88879',
    '9baed511-faf9-47dc-b6ce-6abe3dfbe5ab',
    '9dcd64cf-d753-4c53-87d0-bc011fd94cb3'
  ],
  memo: 'Z',
  **state: 'signed',**//**状态为”signed“**
  sender: '',
  created_at: '2023-07-17T14:47:51.002593Z',
  updated_at: '2023-07-18T04:02:21.547369Z',
  signed_by: '853285a27df68278f0b69417d26507f5f6f3bc12cc1f9e3001b71648e37142b8',
  **signed_tx:** '77770002d4c304ffc3270ee0f3468913bd8027225201f0eccd336d47062d76c6e2b6bb270001d6d3851b9c91172d72a3d948f358b89d8f662e058091dd61e943f39a555e751600010000000000000002000000023a980001f06cce4bb704167f09d05b10df0f739b0bae2959f52859b46d63409f526004d8b7df8ad0338b9dea048de50c0bf2bd57f09142ce18035ec8354385dc1e21175d0003fffe0100000000000402f1c8c00004634fe1c7600a34b399e06f8101d07c66a5b23d0eee4bbf889b9cf2ea4d117cfba8893e5ec2c817055c3a3e9b9445746ee4b9290978d40463edd43a0e6b0b8ec0e575164e6b53c90198a088be4d893f1f2f2f0087d833275afe772dac28563ce74163e7ce8064ec55ad71d975e3f7ef6985a9f9988ea2e11c47060e8d5b889523fe236a0ca2efbd0dd33e6b9606eb69738d27a51667617f7c7da8c35ccc54fde70003fffe03000000015a0000'
}
**第四步执行结果:** 

{
  type: 'multisig_request',
  **request_id: 'a69cee92-d5cb-4db1-99ad-cc3f59e6c2af',**
  user_id: '57915058-dc64-4973-a7ad-5372c0a88879',
  asset_id: '4d8c508b-91c5-375b-92b0-ee702ed2dac5',
  amount: '0.00015',
  threshold: 3,
  senders: [
    '30ec2dc7-76aa-4c3a-83c4-114bbbf3183b',
    '57915058-dc64-4973-a7ad-5372c0a88879',
    '9baed511-faf9-47dc-b6ce-6abe3dfbe5ab',
    '9dcd64cf-d753-4c53-87d0-bc011fd94cb3'
  ],
  receivers: [ '9dcd64cf-d753-4c53-87d0-bc011fd94cb3' ],
  signers: [
    '30ec2dc7-76aa-4c3a-83c4-114bbbf3183b',
    '9baed511-faf9-47dc-b6ce-6abe3dfbe5ab'
  ],
  memo: 'Z',
  action: 'sign',
  **state: 'initial',**
  transaction_hash: '853285a27df68278f0b69417d26507f5f6f3bc12cc1f9e3001b71648e37142b8',
  raw_transaction: '77770002d4c304ffc3270ee0f3468913bd8027225201f0eccd336d47062d76c6e2b6bb270001d6d3851b9c91172d72a3d948f358b89d8f662e058091dd61e943f39a555e751600010000000000000002000000023a980001f06cce4bb704167f09d05b10df0f739b0bae2959f52859b46d63409f526004d8b7df8ad0338b9dea048de50c0bf2bd57f09142ce18035ec8354385dc1e21175d0003fffe0100000000000402f1c8c00004634fe1c7600a34b399e06f8101d07c66a5b23d0eee4bbf889b9cf2ea4d117cfba8893e5ec2c817055c3a3e9b9445746ee4b9290978d40463edd43a0e6b0b8ec0e575164e6b53c90198a088be4d893f1f2f2f0087d833275afe772dac28563ce74163e7ce8064ec55ad71d975e3f7ef6985a9f9988ea2e11c47060e8d5b889523fe236a0ca2efbd0dd33e6b9606eb69738d27a51667617f7c7da8c35ccc54fde70003fffe03000000015a0000',
  created_at: '1970-01-01T00:03:39+00:03',
  code_id: 'c3cb8867-52dc-465a-8dfb-44f3779bbdea'
}

###### **第五步执行结果：完成签名**

 **{**
  type: 'multisig_request',
  request_id: 'a69cee92-d5cb-4db1-99ad-cc3f59e6c2af',
  user_id: '57915058-dc64-4973-a7ad-5372c0a88879',
  asset_id: '4d8c508b-91c5-375b-92b0-ee702ed2dac5',
  amount: '0.00015',
  threshold: 3,
  senders: [
    '30ec2dc7-76aa-4c3a-83c4-114bbbf3183b',
    '57915058-dc64-4973-a7ad-5372c0a88879',
    '9baed511-faf9-47dc-b6ce-6abe3dfbe5ab',
    '9dcd64cf-d753-4c53-87d0-bc011fd94cb3'
  ],
  receivers: [ '9dcd64cf-d753-4c53-87d0-bc011fd94cb3' ],
  signers: [
    '30ec2dc7-76aa-4c3a-83c4-114bbbf3183b',  **//首签**
    '9baed511-faf9-47dc-b6ce-6abe3dfbe5ab',  **// 二签**
    '57915058-dc64-4973-a7ad-5372c0a88879' **// 三签**
  ],
  memo: 'Z',
  action: 'sign',
  **state: 'signed',**
  transaction_hash: '853285a27df68278f0b69417d26507f5f6f3bc12cc1f9e3001b71648e37142b8',
  **raw_transaction:** '77770002d4c304ffc3270ee0f3468913bd8027225201f0eccd336d47062d76c6e2b6bb270001d6d3851b9c91172d72a3d948f358b89d8f662e058091dd61e943f39a555e751600010000000000000002000000023a980001f06cce4bb704167f09d05b10df0f739b0bae2959f52859b46d63409f526004d8b7df8ad0338b9dea048de50c0bf2bd57f09142ce18035ec8354385dc1e21175d0003fffe0100000000000402f1c8c00004634fe1c7600a34b399e06f8101d07c66a5b23d0eee4bbf889b9cf2ea4d117cfba8893e5ec2c817055c3a3e9b9445746ee4b9290978d40463edd43a0e6b0b8ec0e575164e6b53c90198a088be4d893f1f2f2f0087d833275afe772dac28563ce74163e7ce8064ec55ad71d975e3f7ef6985a9f9988ea2e11c47060e8d5b889523fe236a0ca2efbd0dd33e6b9606eb69738d27a51667617f7c7da8c35ccc54fde70003fffe03000000015affffff01e0f9361810300bbd0f0688c6cfe09cbc7fca31df251c80fb2ec8dee038c62fd64e9605be4eb0fbd7d74ee2deb909c5aa92d277434014910b0fa51992668ce80700000107',
  created_at: '2023-07-18T04:02:24.409432Z',
  code_id: 'c3cb8867-52dc-465a-8dfb-44f3779bbdea'
}

**第三签完成签名**



###### 第六步：将签名完成的交易发送给主网 ，将签名广播出去

##### （注：本步骤最后一个签名完成后，将输出raw_transaction:

**执行**：client.sendRawTransaction(raw_transaction）

**输出：**

{
  hash: '853285a27df68278f0b69417d26507f5f6f3bc12cc1f9e3001b71648e37142b8'
}

###### **第七步：查询utxo 获取 状态为”spent“的消息 ，其消息中transaction_hash值与utxo 状态为”unspent“的transaction_hash值相同。**

 {
  type: 'multisig_utxo',
  user_id: '57915058-dc64-4973-a7ad-5372c0a88879',
  utxo_id: '216c0606-84eb-38e3-ad32-adbfb8f68ebd',
  asset_id: '4d8c508b-91c5-375b-92b0-ee702ed2dac5',
  **transaction_hash: 'd6d3851b9c91172d72a3d948f358b89d8f662e058091dd61e943f39a555e7516',**
  output_index: 1,
  amount: '0.49415',
  threshold: 3,
  members: [
    '30ec2dc7-76aa-4c3a-83c4-114bbbf3183b',
    '57915058-dc64-4973-a7ad-5372c0a88879',
    '9baed511-faf9-47dc-b6ce-6abe3dfbe5ab',
    '9dcd64cf-d753-4c53-87d0-bc011fd94cb3'
  ],
  memo: 'Z',
  **state: 'spent',**// **已花销，即已转账到接收者**
  sender: '',
  created_at: '2023-07-17T14:47:51.002593Z',
  updated_at: '2023-07-18T04:02:27.424619Z',
  signed_by: '853285a27df68278f0b69417d26507f5f6f3bc12cc1f9e3001b71648e37142b8',
  signed_tx: '77770002d4c304ffc3270ee0f3468913bd8027225201f0eccd336d47062d76c6e2b6bb270001d6d3851b9c91172d72a3d948f358b89d8f662e058091dd61e943f39a555e751600010000000000000002000000023a980001f06cce4bb704167f09d05b10df0f739b0bae2959f52859b46d63409f526004d8b7df8ad0338b9dea048de50c0bf2bd57f09142ce18035ec8354385dc1e21175d0003fffe0100000000000402f1c8c00004634fe1c7600a34b399e06f8101d07c66a5b23d0eee4bbf889b9cf2ea4d117cfba8893e5ec2c817055c3a3e9b9445746ee4b9290978d40463edd43a0e6b0b8ec0e575164e6b53c90198a088be4d893f1f2f2f0087d833275afe772dac28563ce74163e7ce8064ec55ad71d975e3f7ef6985a9f9988ea2e11c47060e8d5b889523fe236a0ca2efbd0dd33e6b9606eb69738d27a51667617f7c7da8c35ccc54fde70003fffe03000000015affffff01e0f9361810300bbd0f0688c6cfe09cbc7fca31df251c80fb2ec8dee038c62fd64e9605be4eb0fbd7d74ee2deb909c5aa92d277434014910b0fa51992668ce80700000107'
}

​    至此，转账发起、首签、二签、三签，全部由bot通过调用mixin sdk提供的多签API程序完成；查询获得”spent “状态的 utxo消息，检查钱包内的转账记录，其交易hash 与签名hash相符，确认收到由多签钱包转来的”0.00015“USDT。

<img src="https://raw.githubusercontent.com/Dada01Github/images/master/image-20230726221340215.png" alt="image-20230726221340215" style="zoom:50%;" />




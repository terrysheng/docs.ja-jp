---
title: "方法 : ToolStripMenuItems をコピーする | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "メニュー項目、コピーと貼り付け"
  - "MenuStrip コントロール [Windows フォーム]、項目を整理する"
  - "ToolStripMenuItems、コピーと貼り付け"
ms.assetid: 17ef4207-e92e-4db2-b648-27246e6517ad
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 方法 : ToolStripMenuItems をコピーする
デザイン時に、トップレベル メニュー全体とそのサブメニュー項目を、<xref:System.Windows.Forms.MenuStrip> の別の場所にコピーできます。 トップレベル メニュー間で個々のメニュー項目のコピーをすることも、またはメニュー内のメニュー項目の位置を変更することもできます。  
  
### トップレベル メニューとサブメニュー項目を別のトップレベルの場所にコピーするには  
  
1.  コピーするメニューを左クリックして、Ctrl \+ C キーを押します。または、メニューを右クリックして、ショートカット メニューから **\[コピー\]** を選びます。  
  
2.  移動先となる新しい場所の後ろにあるトップレベル メニューを左クリックし、Ctrl \+ V キーを押します。または、移動先となる新しい場所の前にあるトップレベル メニュー項目を右クリックし、ショートカット メニューから **\[貼り付け\]** を選びます。  
  
     選んだトップレベル メニューの前に、コピーしたメニューが挿入されます。  
  
### トップレベル メニューとサブメニュー項目をドロップダウンの場所にコピーするには  
  
1.  移動するメニューを左クリックして、Ctrl \+ C キーを押します。または、メニューを右クリックして、ショートカット メニューから **\[コピー\]** を選びます。  
  
2.  宛先のトップレベル メニューで、移動先となる新しい場所の上にあるサブメニュー項目を左クリックし、Ctrl \+ V キーを押します。または、移動先となる新しい場所の上にあるサブメニュー項目を右クリックし、ショートカット メニューから **\[貼り付け\]** を選びます。  
  
     選んだサブメニュー項目の前に、コピーしたメニューが挿入されます。  
  
### 別のメニューにサブメニュー項目をコピーするには  
  
1.  コピーするサブメニュー項目を左クリックして、Ctrl \+ C キーを押します。または、サブメニュー項目を右クリックして、ショートカット メニューから **\[コピー\]** を選びます。  
  
2.  切り取ったサブメニュー項目を格納するメニューを左クリックします。  
  
3.  移動先となる新しい場所の前にあるサブメニュー項目を左クリックし、Ctrl \+ V キーを押します。または、移動先となる新しい場所の前にあるサブメニュー項目を右クリックし、ショートカット メニューから **\[貼り付け\]** を選びます。  
  
     選んだサブメニュー項目の前に、コピーしたサブメニュー項目が挿入されます。  
  
## 参照  
 <xref:System.Windows.Forms.MenuStrip>   
 <xref:System.Windows.Forms.ToolStripMenuItem>   
 [MenuStrip コントロールの概要](../../../../docs/framework/winforms/controls/menustrip-control-overview-windows-forms.md)
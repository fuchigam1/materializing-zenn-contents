---
title: "[baserCMS]管理側（admin-third）の左メニュー「サイト基本設定」を簡単に表示制御する"
emoji: "🐥"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["baserCMS", "adminthird"]
published: true
---

システム管理ユーザグループ **以外のユーザグループに属する** ユーザでログイン中に、左メニューにある「設定＞サイト基本設定」を消したいな、て思ったときのtips。


## 想定している対象者
- baserCMSでウェブサイトを制作をしている方
- PHPer


### 環境
- baserCMS 4.4.2
- 管理側テーマ: admin-thrid


## 手法1-1: setting.phpの利用
以下のファイルに記述を追加する。

- /app/Config/setting.php

```php
$config['BcApp.adminNavigation.Systems.SiteConfigs.disable'] = true;
```

### 手法1-2: setting.phpの利用＋システム管理ユーザグループ以外のときは消す

```php
if (BcUtil::isAdminSystem(env('REQUEST_URI'))) {
	if (!BcUtil::isAdminUser()) {
		$config['BcApp.adminNavigation.Systems.SiteConfigs.disable'] = true;
	}
}
```


## 手法2-1: プラグインの利用
以下のファイルに記述を追加する。

- app/Plugin/YOUR_PLUGIN/Config/setting.php

```
$config['BcApp.adminNavigation.Systems.SiteConfigs.disable'] = true;
```

### 手法2-2: プラグインの利用＋システム管理ユーザグループ以外のときは消す

```
if (BcUtil::isAdminSystem()) {
	if (!BcUtil::isAdminUser()) {
		$config['BcApp.adminNavigation.Systems.SiteConfigs.disable'] = true;
	}
}
```


## baserCMS Advent Calendar 2020
- Adventar https://adventar.org/calendars/5393

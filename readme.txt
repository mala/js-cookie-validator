これはなに
- Object.definePropertyを使ってdocument.cookieへの書き込みに制約を作ります。
- pathとかdomainとかexpiresを書き換えたり、デフォルト値を指定できます

問題点
- 他のタブ等で設定されたcookieは即座に反映されません
- setIntervalで定期的に再読込されます

サンプル

    CookieValidator.configure({
        debug: true,
        default_path: "/hoge/"
    });
    CookieValidator.set_rule("path", function(key, val, cookie_name, cookie_value){
        console.log(cookie_name +":"+cookie_value + " set to " + val);
        if (val.indexOf("/hoge/") !== 0) {
            console.log("rewrite to /hoge/");
            return [key, "/hoge/"];
        }
    });
    CookieValidator.on();


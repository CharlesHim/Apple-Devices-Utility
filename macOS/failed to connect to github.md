- 清除代理设置：  

```
git config --global --unset http.proxy
git config --global --unset https.proxy
```



- 重设代理：  

```
# using socks proxy
git config --global http.proxy "socks5://127.0.0.1:1080"
git config --global https.proxy "socks5://127.0.0.1:1080"

# using http or https proxy
git config --global http.proxy "http://127.0.0.1:8080"
git config --global https.proxy "https://127.0.0.1:8080"
```

> 注意，端口要换成自己的代理的端口。

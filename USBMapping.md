先上诊断报告
```
  #######################################################
 #                  Port Discovery                     #
#######################################################

Intel(R) USB 3.20 可扩展主机控制器 - 1.20 (Microsoft) | USB 3.0 (XHCI) | 25 ports
  Port 1 | USB 2.0 | Type C - with switch (guessed)
  Port 2 | USB 2.0 | Internal (guessed)
    - MYSTIC LIGHT - operating at USB 1.1
  Port 3 | USB 2.0 | Internal (guessed)
    - USB2.1 Hub - operating at USB 2.0
      - USB Hub 2.0 - operating at USB 1.1
        - USB-HID Keyboard - operating at USB 1.1
      - USB2734 - operating at USB 2.0
        - USB Receiver - operating at USB 1.1
        - Hub Controller - operating at USB 2.0
  Port 4 | USB 2.0 | Type C - with switch (guessed)
  Port 5 | USB 2.0 | Type A (guessed)
  Port 6 | USB 2.0 | Type A (guessed)
  Port 7 | USB 2.0 | Type A (guessed)
  Port 8 | USB 2.0 | Type A (guessed)
  Port 9 | USB 2.0 | USB 3 Type A (guessed)
  Port 10 | USB 2.0 | USB 3 Type A (guessed)
  Port 11 | USB 2.0 | Internal (guessed)
    - USB2.0 Hub - operating at USB 2.0
  Port 12 | USB 2.0 | Internal (guessed)
  Port 13 | USB 2.0 | Internal (guessed)
  Port 14 | USB 2.0 | Internal (guessed)
    - 英特尔(R) 无线 Bluetooth(R) - operating at USB 1.1
  Port 15 | USB 2.0 | Type A (guessed)
  Port 16 | USB 2.0 | Type A (guessed)
  Port 17 | USB 3.0 | Type C - with switch (guessed)
  Port 18 | USB 3.0 | Internal (guessed)
    - USB3.2 Hub - operating at USB 3.1 Gen 2
      - USB5734 - operating at USB 3.0
  Port 19 | USB 3.0 | Type C - with switch (guessed)
    - Ugreen Storage Device - operating at USB 3.1 Gen 2
  Port 20 | USB 3.0 | Internal (guessed)
  Port 21 | USB 3.0 | Internal (guessed)
  Port 22 | USB 3.0 | Internal (guessed)
  Port 23 | USB 3.0 | Internal (guessed)
  Port 24 | USB 3.0 | USB 3 Type A (guessed)
  Port 25 | USB 3.0 | USB 3 Type A (guessed)
    - DataTraveler 3.0 - operating at USB 3.0
```

这块主板是一供25个接口，参考(抄:>)一位yzchan大神的  [`Mapper`](https://github.com/yzchan/MSI-MAG-B660M-MORTAR-DDR4-12600K-EFI/blob/master/USB%E5%AE%9A%E5%88%B6.md) 列出表格

| Port | Companion | 描述                | 选择|
|------|-----------|-------------------| ----|
| 1    | 17        | 后面板Type-C(USB2.0) | 
| 2    |           | MSI灯效调节功能         | x|
| 3    | *18       | 后面板Type-A(USB2.0) | x
| 4    | 19        | JUSB4(USB2.0)     | x
| 5    |           | 后面板USB2.0         | x
| 6    |           | 后面板USB2.0         | x
| 7    |           | 后面板USB2.0         | x
| 8    |           | 后面板USB2.0         | x
| 9    | 24        | JUSB3 (USB2.0)    | x
| 10   | 25        | JUSB3 (USB2.0)    | x
| 11   |           | JUSB1/JUSB2       | x
| 12   |           | -                 |
| 13   |           | -                 |
| 14   |           | 英特尔(R) 无线 Bluetooth(R)| x 
| 15   |           | -                 |
| 16   |           | -                 |
| 17   | 1         | 后面板Type-C(USB2.0) | 
| 18   | *3        | 后面板Type-A         | x
| 19   | 4         | JUSB4(USB3.0)     | x
| 20   |           | -                 |
| 21   |           | -                 |
| 22   |           | -                 |
| 23   |           | -                 |
| 24   | 9         | JUSB3             | x
| 25   | 10        | JUSB3                 | x

我按照我当前机箱做了调整，主要是前置的USB口[`JUSB3`]有两个A口、一个Type-C口，所以在不影响使用的前提下我对USB重新进行了分配。
目前端口可用，但是最大只能是定义到15口的系统限制，待后续看看有什么别的办法。
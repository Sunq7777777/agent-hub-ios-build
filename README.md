# Agent Hub iPhone 云端打包

该流程使用 GitHub 托管的 Mac 构建真实 iPhone 的 arm64 IPA，本机不需要安装 Xcode。

源码固定为 easyaigc/agent-hub 的 `c66f3cd6db34c7992fa033f817d6eb508a0383bd`。源码只读检出，不修改原项目或使用原作者的签名凭据。

将 `.github/workflows/build-iphone.yml` 放入自己有写权限、启用 Actions 的专用 GitHub 仓库。提交到 main 会启动一次构建；后续也可在 Actions 手动执行 Build Agent Hub for iPhone。推荐使用专用公开仓库，内容仅包含此公开源码的构建配置，不上传 Apple 账号或设备信息。

构建成功后下载 `AgentHub-iPhone` artifact，其中包含 `AgentHub-iPhone-unsigned.ipa`、SHA-256、源码指纹和构建信息。该 IPA **尚未签名**，需要通过 Sideloadly 等方式签名后安装；它不是 TestFlight 或可直接点链接安装的 Ad Hoc 包。

原项目的主应用和扩展保持完整。普通免费 Apple 账号的权限兼容性、扩展及推送功能需要安装时核实；不要把云端编译成功当成真机功能验收通过。Apple 账号密码和验证码由本人在安装工具中输入，不上传到 GitHub。

构建仓库：https://github.com/Sunq7777777/agent-hub-ios-build

## 安装前需要准备

- iPhone 使用 iOS 17 或更新版本。
- 用于个人签名的 Apple 账号。密码与验证码由本人在安装工具中输入。
- 首次使用 Sideloadly 无线安装，需要先通过支持数据传输的 USB 线将 iPhone 与这台 Mac 配对，并在 Finder 开启“在 Wi-Fi 下显示此 iPhone”。隔空投送只能传文件，不能完成签名和安装。
- 免费 Apple 账号签名通常有效 7 天，之后需要重新签名；Sideloadly 可以在电脑与手机连接时刷新。

安装工具官方说明：https://sideloadly.io/faq

每次构建是否成功以仓库 Actions 页面为准。只有运行成功并生成 `AgentHub-iPhone` artifact 后才可下载 IPA；实际手机安装和功能仍需另外核实。

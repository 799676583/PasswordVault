# Password Vault — 更新器 1.0.1

Windows 更新器及 STM32U083CCT6 签名固件发布仓库。

> 当前版本仍处于实板验证阶段：已确认测试板保护与启动验签；保护后的完整升级及维修流程尚未验证完成。发行号 1.0.0 不代表量产认证。

## 下载

- [Windows 更新器 1.0.1](PasswordVaultUpdate-v1.0.1.exe)（进入文件页面后下载原始文件）
- [签名固件 1.0.0](firmware/vault.pvfw)
- [SHA256 清单](SHA256.md)

内部安全版本为 1。EXE 内置相同的签名固件；选择外部包时使用 firmware/vault.pvfw。

## 更新

1. 连接已安装安全引导程序且已完成保护配置的设备，长按滚轮约 6 秒进入安全更新模式。
2. 打开更新器，查看目标版本及更新说明。
3. 将以下 **固件包 SHA256** 粘贴到核对框（不是 EXE 的摘要）：

```text
a1729df27c14bdcdd76050cbe9a23580d60fd0c662e784de9c9d304d04187f98
```

4. 点击更新设备，按设备提示输入 PIN，期间保持供电。
5. 等待完成及自动重启，再核对原 PIN 和原有测试记录。

如报错，保留命令/偏移等信息，先取消本次更新后重新授权。不要把失败视为完成。尚未擦写时可拔插退出更新模式；应用已擦写但未完成时，需要成功重传有效固件才能恢复应用。

六次连续错误 PIN 会清空记录。PIN 仅在设备输入。设备仍会检查固件数字签名和安全版本；SHA256 不能代替验签。

## 更新器 1.0.1

修复“更新设备”按钮显示不完整：独立底部操作栏、可滚动内容及可调整窗口大小。本次仅升级更新器，仓库内置固件仍为 1.0.0；已升级设备请手动选择相应的新固件包，不要使用旧包降级。

## 更新内容

- 固件：签名升级与设备 PIN 授权，保留记录区；沿用当前签名固件内容。
- 更新器：展示目标版本和更新说明，强制核对分发 SHA256；暂时读取失败时限时等待原命令响应，不重发擦写命令。

## 仓库范围

仅包含发布用 EXE、签名固件和说明。首次安装镜像、首次烧写脚本、设备数据、维修工具、签名私钥、源工程及原项目 Git 历史均不在本仓库中。本仓库不能用于空白板首次安装。

## 上传这个本地仓库

GitHub **Import repository** 需要已有远程仓库 URL，不接受本地 ZIP。参见 [GitHub 官方说明](https://docs.github.com/en/migrations/importing-source-code/using-github-importer/importing-a-repository-with-github-importer)。

本地仓库上传方法：在 GitHub 新建空仓库，不初始化 README/License/gitignore；在解压后的本文件所在目录运行（替换为你自己的地址）：

```powershell
git remote add origin https://github.com/YOUR-USER/password-vault-release.git
git push -u origin main
git push origin v1.0.0
```

也可以用 GitHub Desktop 的 Add Local Repository 打开此目录再发布。本地 ZIP 包含独立的 .git 历史；无需复制原硬件项目。若使用网页 Upload files，应上传仓库文件内容，不要上传 .git 文件夹或只上传整个 ZIP。

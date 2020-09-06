## Setting up clang-format (Windows)
- Load `cmd` as Administrator.
- Install `choco` package manager with script below:
```cmd
@"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command " [System.Net.ServicePointManager]::SecurityProtocol = 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"
```
- Install LLVM
```cmd
choco install llvm -y
curl.exe --output C:\Program Files\LLVM\bin\clang-format-diff.py --url https://raw.githubusercontent.com/llvm-mirror/clang/master/tools/clang-format/clang-format-diff.py
refreshenv
```

## Setting up clang-format (Linux)
```bash
sudo apt install clang-format
```

## Using clang-format
- To get a report of what (in your current changes) needs formatting:
```bash
git diff -U0 --no-color release...HEAD -- '*.cpp' '*.h' | clang-format-diff -p1
```
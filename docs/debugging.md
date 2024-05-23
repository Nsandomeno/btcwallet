# Work with BtcWallet in Debug Mode
This is specific to VS Code. May still need to 
rebuild the binary for changes.

# Step 1 - Create .vscode Directory at Root of Repository
Then add a `launch.json` file

`mkdir .vscode`

`touch launch.json`

Copy the following content to the `launch.json`

```
{
    "configurations": [
    {
            "name": "Launch file",
            "buildFlags": [],
            "type": "go",
            "request": "launch",
            "mode": "exec",
            "program": "./btcwallet",
            "args": ["--configfile=~/Library/Application Support/Btcwallet/Btcwallet.conf", "--rpclisten=127.0.0.1:18332"]
            }
    ]   
}
```

# Step 2 - Build the Golang Binary
`make build`

Copy the binary from where your system is setup to store
its Go binaries to the root of the repository. This is because there is an issue with getting the debug config to 
read files above it in the file structure it lives in.

`cp ~/go/bin/btcwallet ./btcwallet`

# Step 3 - Run in Debug Mode
Open `./btcwallet.go` in VS Code and click then Run > Start Debugging.
## Prerequisites

- [Golang Cobra Installed](https://github.com/spf13/cobra)
- [Viper Installed](https://github.com/spf13/viper)
- [The Need Of Using Environment Variables](https://12factor.net/config)

Let's go

Prepare your working directory, (new folder)

```
cobra init appname
```

Or include config file directly

```
cobra init appname --config appname.yaml
```

Create the .yaml file

In the root.go file, there is initConfig() function.
set the .yaml as the configuration

```go
func initConfig() {
  fmt.Println("Init CONFIG ")
  workingdir, err := os.Getwd()
  cobra.CheckErr(err)
  viper.SetConfigFile(workingdir + "/appname.yaml")
  if err := viper.ReadInConfig(); err != nil {
    fmt.Printf("Error reading config file, %s", err)
  }

  viper.AutomaticEnv()
  // If a config file is found, read it in.
  if err := viper.ReadInConfig(); err == nil {
    fmt.Fprintln(os.Stderr, "Using config file:", viper.ConfigFileUsed())
  }
}
```

Call the .yaml key like this

```
viper.GetBool("KEY")
viper.GetString("KEY")
viper.GetInt("KEY")
```

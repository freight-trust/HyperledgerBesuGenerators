# Besu Plugins API Demo Plugin

This sample project is modified from https://github.com/PegaSysEng/PluginsAPIDemo

## Purpose of the Demo Plugin

Expose finer grain details about the gas usage in blocks via Prometheus

### Services Used

- **PicoCLIOptions**
  - To add configuration options to change the name of the metrics
- **MetricCategoryRegistry** and **MetricsSystem**
  - To add the metrics to the metrics endpoint
- **BesuEvents**
  - To listen to propagated blocks and capture relevant data

### Plugin Lifecycle

- **Register**
  - Add the configuration options and metrics category
- **Start**
  - Connect to the Besu events
- **Stop**
  - Disconnect from the Besu events

## To Execute the Demo in a Container with Iterative Development

If this project was initialized from Appsody, run the stack

```
appsody run
```

Then go to http://localhost:9545/metrics to see the metrics.

Any changes you make to Java files or build.gradle will be automatically redeployed to the container within seconds. Refresh http://localhost:9545/metrics to see your updates.

## To Execute the Demo Locally

Build the plugin jar

```
./gradlew build
```

Install the plugin into `$BESU_HOME`

```
mkdir $BESU_HOME/plugins
cp build/libs/*.jar $BESU_HOME/plugins
```

Run the Besu node w/o customized metric names

```
$BESU_HOME/bin/besu --config-file=demo-options.toml
```

Then go to http://localhost:9545/metrics to see the metrics

To change the names of the metrics use the plugin CLI options

```
$BESU_HOME/bin/besu --config-file=demo-options.toml \
  --plugin-gas-spending-metrics-name=a_name
  --plugin-gas-spending-metrics-prefix=a_prefix_
```

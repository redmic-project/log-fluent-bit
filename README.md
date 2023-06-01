# Fluent Bit

Configure and deploy Fluent Bit, a lightweight service to ingest logs and feed Loki

## Log level recognition

There are 6 log levels to be recognised (inspired by [Grafana](https://grafana.com/docs/grafana/latest/explore/logs-integration/#log-level)): `critical`, `error`, `warning`, `info`, `debug` and `trace`.

If none of them is recognised, then no `level` label is applied to log message. This way, another tool (like Grafana Logs Panel) may infer it's level later.

Detection is based on finding a **field** with level value or a level value between **delimiters**.

You can customise detected log level values setting these environment variables:

| Variable name | Default value |
| - | - |
| LOG_LEVEL_CRITICAL_VALUES | emerg\|fatal\|alert\|crit\|critical\|Emerg\|Fatal\|Alert\|Crit\|Critical\|EMERG\|FATAL\|ALERT\|CRIT\|CRITICAL |
| LOG_LEVEL_ERROR_VALUES | eror\|err\|error\|Eror\|Err\|Error\|EROR\|ERR\|ERROR |
| LOG_LEVEL_WARNING_VALUES | warn\|warning\|Warn\|Warning\|WARN\|WARNING |
| LOG_LEVEL_INFO_VALUES | info\|information\|informational\|notice\|Info\|Information\|Informational\|Notice\|INFO\|INFORMATION\|INFORMATIONAL\|NOTICE |
| LOG_LEVEL_DEBUG_VALUES | dbug\|debug\|Dbug\|Debug\|DBUG\|DEBUG |
| LOG_LEVEL_TRACE_VALUES | trace\|Trace\|TRACE |

Also, you can change detected field names and delimeters using these environment variables:

| Variable name | Default value |
| - | - |
| LOG_LEVEL_FIELDS | level=\|lvl=\|Level=\|Lvl=\|LEVEL=\|LVL= |
| LOG_LEVEL_DELIMITERS | \d\|\W\|\dm |

> Value `\dm` used at `${LOG_LEVEL_DELIMITERS}` allows recognising coloured logs with ANSI codes (ending with an integer followed by `m`).

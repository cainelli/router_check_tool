# router_check_tool

Envoy [route table check tool](https://www.envoyproxy.io/docs/envoy/latest/operations/tools/route_table_check_tool.html) container image.

```shell
docker run --rm -v $(pwd)/examples:/examples  cainelli/router_check_tool  -c examples/routes.json -t examples/test.json
```

-   [v1.15.x](https://github.com/cainelli/router_check_tool/tree/v1.15.x)

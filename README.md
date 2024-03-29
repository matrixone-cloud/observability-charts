# Observability
MOCloud Observability Charts

# Scrape

[Scrape List](./docs/scrape/README.md) 

## 如何添加新的采集任务

 在业务代码中引入prometheus的指标抓取接口，详情请参考：[业务 metric 采集接入](https://github.com/matrixone-cloud/observability-charts/wiki/%E4%B8%9A%E5%8A%A1-metric-%E9%87%87%E9%9B%86%E6%8E%A5%E5%85%A5)

为了便于prometheus的服务发现，在k8s上需要部署组件相对应的 `service` （推荐），部署好service后，可以去相应集群的grafana页面中看看是否已经有开始采集到数据（可能会有2-3分钟的延迟），不同集群的grafana环境以及账号请见：[Grafana 地址列表](https://doc.weixin.qq.com/doc/w3_AW0A-gb6AOIAWdUX2NbSWevRb4vhF?scode=AJsA6gc3AA8iTHdq3jAW0A-gb6AOI)


# Alerts

- [Alerts List](./docs/alerts/README.md)


值得注意的是，所有在上面流程创建的新文件都需要在在 `.github/CODEOWNERS` 下以 `[文件名] [@github名]` 标注文件的 owner

## 如何提交新的告警规则

为了为你的应用接入监控并告警，需要完成以下工作：

 1. 业务端暴露 /metrics 接口接入采集：[如何添加新的采集任务](#%E5%A6%82%E4%BD%95%E6%B7%BB%E5%8A%A0%E6%96%B0%E7%9A%84%E9%87%87%E9%9B%86%E4%BB%BB%E5%8A%A1)
 2. 编写告警规则 & 告警单元测试并验证：[编写告警规则与告警单元测试](https://github.com/matrixone-cloud/observability-charts/wiki/MO%E2%80%90OB-告警接入操作流程#3-编写告警规则与告警单元测试)
 3. [可选] 添加 Alertmanager Receiver 配置并验证：[Alertmanager Receiver 配置与验证](https://github.com/matrixone-cloud/observability-charts/wiki/MO%E2%80%90OB-告警接入操作流程#4--可选-alertmanager-receiver-配置与验证)
 4. [可选] Grafana Dashboard 本地调试：[Grafana 本地调试](https://github.com/matrixone-cloud/observability-charts/wiki/MO%E2%80%90OB-告警接入操作流程#4--可选-添加-grafana-dashboard-并本地调试)
 5. [可选] 添加 Grafana Dashboard 信息：[如何提交新的 Dashboards 配置](#%E5%A6%82%E4%BD%95%E6%8F%90%E4%BA%A4%E6%96%B0%E7%9A%84-dashboards-%E9%85%8D%E7%BD%AE)
 6. 提交 PR ，根据 PR 模板添加相关 README 说明

详细 Workaround：[MO‐OB 告警接入操作流程](https://github.com/matrixone-cloud/observability-charts/wiki/MO%E2%80%90OB-%E5%91%8A%E8%AD%A6%E6%8E%A5%E5%85%A5%E6%93%8D%E4%BD%9C%E6%B5%81%E7%A8%8B)

# Dashboards
- [details](./docs/dashboards)

- [dashboard config list](./charts/mo-ruler-stack/grafana/dashboards/README.md)

## 如何提交新的 Dashboards 配置
1. 绘制: 请在 grafana web UI上绘制你的 dashboard
2. 下载dashboard.json配置: 请在 dashboard展示页 => setting => JSON Model => Save as => save on your PC.
3. 提交PR: 请将 dashboard.json 提交至目录 [charts/mo-ruler-stack/grafana/dashboards](./charts/mo-ruler-stack/grafana/dashboards), 并追加 [dashboards list](./charts/mo-ruler-stack/grafana/dashboards/README.md)

提交前请注意以下细节
1. dashboard 标题, 推荐使用 `{模块}/{分类 or 服务}`
    - 模块 取值: [ kubernetes, Node Exporter, Prometheus, MOCloud ]
    - 分类 or 服务:  可参考目前取值 [dashboards list](./charts/mo-ruler-stack/grafana/dashboards/README.md)
2. dashboard.json 文件名, 同样推荐使用 `{模块}/{分类 or 服务}.json`
    - 例如: moc-auth-service.json 对应: `MOCloud / Auth-Service` metric指标
    - 详见目前支持的 [dashboards list](./charts/mo-ruler-stack/grafana/dashboards/README.md)
3. 在 `.github/CODEOWNERS` 下以 `[文件名] [@github名]` 标注dashboard文件的创建人

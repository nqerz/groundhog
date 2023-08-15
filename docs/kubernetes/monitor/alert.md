# Alarm

Use webhook to extend alert channel is flexible and easy to expand.

## Alarm system should contains following features

- Alarm source management, that is, docking with multiple platforms
- Alarm channel management, that is, docking multiple channels according to user requirements: Dingtalk, Slack, WeChat, EMail, Phone Call, etc.
- On-duty management, arrange on-duty personnel according to time slots or certain rules, my understanding is mainly time-based scheduling management.
- User management, including: contact information, time zone, language, etc.
- Alarm suppression, grouping, silence function

## Commercial solutions

Products:

- [Pagerduty](https://www.pagerduty.com/)
- [Opsgien](https://www.atlassian.com/software/opsgenie)
- [ILert](https://www.ilert.com/)

Personal opinion:

- Pagerduty has a wide range of users.
- OPsgien: good integrated with Jira, confluence's products.
- ILert similar to Pagerduty.

## Opensource solutions

- [Alertmanager](https://prometheus.io/docs/alerting/latest/alertmanager/)
- [Zabbix](https://www.zabbix.com/)
- [PrometheusAlert](https://github.com/feiyu563/PrometheusAlert)

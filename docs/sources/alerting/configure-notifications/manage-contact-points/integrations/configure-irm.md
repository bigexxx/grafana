---
aliases:
  - ../../../configure-notifications/manage-contact-points/integrations/configure-oncall/ # /docs/grafana/<GRAFANA_VERSION>/alerting/configure-notifications/manage-contact-points/integrations/configure-oncall/
  - ../../../alerting-rules/manage-contact-points/configure-oncall/ # /docs/grafana/<GRAFANA_VERSION>/alerting/alerting-rules/manage-contact-points/configure-oncall/
  - ../../../alerting-rules/manage-contact-points/integrations/configure-oncall/ # /docs/grafana/<GRAFANA_VERSION>/alerting/alerting-rules/manage-contact-points/integrations/configure-oncall/
  - ../configure-oncall/ # /docs/grafana/<GRAFANA_VERSION>/alerting/alerting-rules/manage-contact-points/configure-oncall/
canonical: https://grafana.com/docs/grafana/latest/alerting/configure-notifications/manage-contact-points/integrations/configure-irm/
description: Configure the Alerting - Grafana IRM integration to connect alerts generated by Grafana Alerting with Grafana IRM
keywords:
  - grafana
  - alerting
  - oncall
  - irm
  - integration
labels:
  products:
    - oss
    - enterprise
menuTitle: Grafana IRM
title: Configure Grafana IRM for Alerting
weight: 120
refs:
  configure-contact-points:
    - pattern: /docs/grafana/
      destination: /docs/grafana/<GRAFANA_VERSION>/alerting/configure-notifications/manage-contact-points/
    - pattern: /docs/grafana-cloud/
      destination: /docs/grafana-cloud/alerting-and-irm/alerting/configure-notifications/manage-contact-points/
  irm:
    - pattern: /docs/
      destination: /docs/grafana-cloud/alerting-and-irm/irm/
  irm-alert-templates:
    - pattern: /docs/
      destination: /docs/grafana-cloud/alerting-and-irm/irm/configure/escalation-routing/alert-templates/
  irm-escalation-chains:
    - pattern: /docs/
      destination: /docs/grafana-cloud/alerting-and-irm/irm/configure/escalation-routing/escalation-chains/
  irm-configure-integrations:
    - pattern: /docs/
      destination: /docs/grafana-cloud/alerting-and-irm/irm/configure/integrations/configure-integrations/
  webhook-contact-point:
    - pattern: /docs/grafana/
      destination: /docs/grafana/<GRAFANA_VERSION>/alerting/configure-notifications/manage-contact-points/integrations/webhook-notifier
    - pattern: /docs/grafana-cloud/
      destination: /docs/grafana-cloud/alerting-and-irm/alerting/configure-notifications/manage-contact-points/integrations/webhook-notifier
  webhook-json-payload:
    - pattern: /docs/grafana/
      destination: /docs/grafana/<GRAFANA_VERSION>/alerting/configure-notifications/manage-contact-points/integrations/webhook-notifier/#json-payload
    - pattern: /docs/grafana-cloud/
      destination: /docs/grafana-cloud/alerting-and-irm/alerting/configure-notifications/manage-contact-points/integrations/webhook-notifier/#json-payload
  irm-contact-point-in-gc:
    - pattern: /docs/
      destination: /docs/grafana-cloud/alerting-and-irm/alerting/configure-notifications/manage-contact-points/integrations/configure-irm
---

[//]: <> (The IRM instructions are different for Grafana Cloud, so this page is currently skipped from Cloud docs.)

# Configure Grafana IRM for Alerting

In Grafana OSS and Grafana Enterprise, you can use a webhook contact point to send alerts to [Grafana IRM](ref:irm). Grafana IRM can then route alerts based on escalation chains for your team's workflows.

The alert notification flow is as follows:

<sup>\*</sup> **Grafana OSS/Enterprise** (send webhook alerts)->**Grafana Cloud IRM** (route via [escalation chains](ref:irm-escalation-chains))

{{< admonition type="note" >}}

The Free Forever plan in Grafana Cloud IRM includes 3 IRM active users per month.

These instructions apply only to Grafana OSS and Grafana Enterprise. To configure IRM for Grafana Cloud Alerting, refer to the [Grafana Cloud documentation](ref:irm-contact-point-in-gc).

{{< /admonition >}}

## Configure an integration in Grafana IRM

First, enable an integration in IRM to accept alerts from Grafana Alerting. You can either create a new integration or use an existing **Alertmanager** or **Webhook** integration in IRM.

To create the integration, follow the same steps as described in [Configure an OnCall integration in IRM](ref:irm-configure-integrations):

1. Navigate to **Alerts & IRM** -> **IRM** -> **Integrations**.
1. Click **+ New integration**.
1. Select either **Alertmanager** or **Webhook** integration from the list.

   - **Alertmanager** integration – Includes preconfigured IRM templates for processing Grafana and Prometheus alerts.

     > The **Grafana Alerting** integration works similarly but may display a warning in the UI.

   - **Webhook** integration – Uses default IRM templates for general alert processing.

1. Provide a title, description, and assign it to a team, then click **Create Integration**.
1. On the integration details page, copy the **HTTP Endpoint** URL to use in the next section.

## Configure a webhook contact point in Grafana Alerting

Next, configure the contact point in Grafana Alerting to send alert notifications to Grafana IRM.

In **Grafana OSS** and **Grafana Enterprise**, you need to create a **Webhook** contact point using the HTTP endpoint URL you copied in the previous step.

1. Navigate to **Alerts & IRM** -> **Alerting** -> **Contact points**.
1. Click **+ Add contact point**.
1. Enter a name for the contact point.
1. From the **Integration** list, select **Webhook**.
1. In the **URL** field, enter the HTTP endpoint URL of the IRM integration.
1. Click **Save contact point**.

After configuring the contact point in Grafana Alerting and the integration in Grafana IRM, you can start testing the Alerting-to-IRM integration.

For more information, see:

- **[Configure contact points](ref:configure-contact-points)** – Learn how to test the integration and enable notifications in Alerting.
- **[Webhook contact point](ref:webhook-contact-point)** – Learn the format of the webhook payload and additional settings in Alerting.
- **[Configure IRM alert templates](ref:irm-alert-templates)** – Learn how to process the incoming webhook messages in IRM.

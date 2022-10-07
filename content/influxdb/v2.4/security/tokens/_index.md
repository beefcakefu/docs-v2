---
title: Manage API tokens
seotitle: Manage API tokens in InfluxDB
description: Manage API tokens in InfluxDB using the InfluxDB UI or the influx CLI.
aliases:
  - /influxdb/v2.4/users/tokens
influxdb/v2.4/tags: [tokens, authentication, security]
menu:
  influxdb_2_4:
    name: Manage tokens
    parent: Security & authorization
weight: 104
---

InfluxDB **API tokens** ensure secure interaction between InfluxDB and external tools such as clients or applications.

Learn how to create, view, update, or delete an API token.

## Authorizations and API tokens

InfluxDB uses API tokens to authenticate and authorize `influx` CLI commands
and InfluxDB `/api/v2` API requests.
In InfluxDB, an _authorization_ associates an API token, a [user](influxdb/v2.4/reference/glossary/#user), and a list of read-write resource permissions.
Any client that authenticates with an API token is granted the permissions associated
with that token.
A user that authenticates with username and password is granted the permissions
of all the API tokens that the user owns.
## API token types

When you create an API token, you specify the permissions for the token.
The InfluxDB UI and `influx` CLI let you create tokens that have
predefined permissions lists for instance owners and organization admins.
The following token "types" describe the permissions granted by the token:

- [Operator API token](#operator-token)
- [All-Access API token](#all-access-token)
- [Read/Write token](#readwrite-token)

#### Operator token

An _Operator token_ grants the following access:

- Full `read` and `write` permissions to **all organizations and all organization resources in InfluxDB OSS 2.x**.
- _Instance owner_ permission.
- Permission to create Operator tokens.

Some operations require the Operator token for _instance owner_ permission--for example, [retrieving the server configuration](/influxdb/v2.4/reference/config-options/).
During the setup process, InfluxDB creates an Operator token owned by the initial user.
To [create an operator token manually](/influxdb/v2.4/security/tokens/create-token/) with the InfluxDB UI, `api/v2` API, or `influx` CLI after the setup process is completed, you must use an existing operator token.

To create a new operator token without using an existing one, see how to use the [`influxd recovery auth`](/influxdb/v2.4/reference/cli/influxd/recovery/auth/) CLI.

{{% note %}}
Because Operator tokens have full read and write access to all organizations in the database,
we recommend [creating an All-Access token](/influxdb/v2.4/security/tokens/create-token/)
for each organization and using those to manage InfluxDB.
This helps to prevent accidental interactions across organizations.
{{% /note %}}

#### All-Access token
Grants full read and write access to all resources in an organization.

#### Read/Write token
Grants read access, write access, or both to specific buckets in an organization.

{{< children hlevel="h2" >}}

---
layout:
  width: default
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
  tags:
    visible: true
---

# Setup Wizard Workflow

The Setup Wizard is a build-in feature that guides the user through the initial setup process. This page documents the protocol that underlies the setup wizard functionality.

When a WebSocket connection is first established to the TVH server, an array of unsolicited messages is received.

A message with a `notificationClass` property of type `accessUpdate` should be present in that array.  If there is a  `wizard` property present in that message, it will contain the name of the current wizard step.

This information can also be obtained from `comet/poll/.`\
**Note:** No `/api/` prefix.

Valid steps are:

<table><thead><tr><th width="133">Step Name</th><th>Wizard Operation</th></tr></thead><tbody><tr><td>"hello"</td><td>Language selection.</td></tr><tr><td>"login"</td><td>Computer Network, Admin and User details.</td></tr><tr><td>"network"</td><td>TVH Network Type to Adaptor mapping.</td></tr><tr><td>"muxes"</td><td>Pre-defined mux selection, per TVH Network type.</td></tr><tr><td>"status"</td><td>Service scanning underway.</td></tr><tr><td>"mapping"</td><td>Service Mapping and Tag creation.</td></tr><tr><td>"channels"</td><td>This is the 'Finished' screen.</td></tr></tbody></table>

At each step, there is a corresponding 'load' and 'save' operation.

**For example:**

`/api/wizard/login/load`\
`/api/wizard/login/save`

Each 'load' operation retrieves the fields that are required for that step and the 'save' operation returns the values of those fields.

**Sample response for '/api/wizard/login/save':**

`{`\
&#x20;   `"network":"0.0.0.0/0",`\
&#x20;   `"admin_username":"admin_user",`\
&#x20;   `"admin_password":"admin_password",`\
&#x20;   `"username":"normal_user",`\
&#x20;   `"password":"normal_password",`\
&#x20;   `"uuid":"00000000000000000000000000000000"`\
`}`

The wizard can be manually started with a `/api/wizard/start` operation. This operation resets the 'wizard' property to "hello".

The wizard can be manually stopped with a `/api/wizard/cancel` operation. This operation removes the 'wizard' property.

**Outstanding Research:**

* Error messages
* Data validation
* Scan status progress updates


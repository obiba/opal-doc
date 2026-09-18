DataSHIELD Quota
================

Manage the DataSHIELD usage quotas: list the quotas if no option is provided, otherwise fetch, add, update or delete a quota, or report what a user has consumed against the quota that applies to them.

A quota is an allowance of R usage granted to a subject (the system default, a group or a user) for a usage metric. What is consumed against it is summed over the rolling window of the quota period: there is no reset instant, capacity returns as old activity ages out.

.. code-block:: bash

  opal datashield-quota <CREDENTIALS> [OPTIONS] [EXTRAS]

Options
-------

==================================== =====================================
Option                               Description
==================================== =====================================
``--id ID, -id ID``                  Quota identifier. Not specifying the quota identifier, will get the list of the DataSHIELD quotas.
``--fetch, -fe``                     Fetch one or multiple quota(s). This is the default action.
``--add, -a``                        Add a quota
``--update, -ud``                    Update the quota specified by the --id option
``--delete, -de``                    Delete the quota specified by the --id option
``--usage, -us``                     Get the quota usage of the user specified by the --subject option, or of the current user when omitted
``--type TYPE, -ty TYPE``            Subject type: ``system``, ``group`` or ``user``. Default is ``system``.
``--subject SUBJECT, -s SUBJECT``    Subject name: the user or the group name (required when the subject type is ``user`` or ``group``)
``--metric METRIC, -m METRIC``       Usage metric: ``execution-time`` or ``session-time``. Default is ``execution-time``.
``--period PERIOD, -pd PERIOD``      Rolling period the usage is summed over: ``daily`` or ``weekly``. Default is ``weekly``.
``--limit LIMIT, -lm LIMIT``         Usage allowance, in minutes (zero forbids DataSHIELD for this subject)
``--disabled, -di``                  Disable the quota (on add, if omitted the quota is enabled by default)
``--enabled, -en``                   Enable the quota (on update, when neither --enabled nor --disabled is specified, the quota is left as it is)
==================================== =====================================

.. note::
  A subject can be given one quota per metric: ``execution-time`` bills the R server's CPU the user consumed and prices an idle session at zero, whereas ``session-time`` bills the R server they are holding whether it computes or not.

  The quota that applies to a user is their own if they have one, else the most permissive of the ones given to the groups they belong to, else the system default. A disabled quota is not a quota: the search falls through to the next one. Having no quota at all means unlimited usage.

.. include:: ../common-credentials.rst

.. include:: ../common-extras-json.rst

Example
-------

List the DataSHIELD quotas:

.. code-block:: bash

  opal datashield-quota --opal https://opal-demo.obiba.org --user administrator --password password --json

Get a specific quota:

.. code-block:: bash

  opal datashield-quota --opal https://opal-demo.obiba.org --user administrator --password password --fetch --id 1

Set the system default to 3 hours of execution time per week:

.. code-block:: bash

  opal datashield-quota --opal https://opal-demo.obiba.org --user administrator --password password --add --limit 180

Give the group ``researchers`` 8 hours of session time per day:

.. code-block:: bash

  opal datashield-quota --opal https://opal-demo.obiba.org --user administrator --password password --add --type group --subject researchers --metric session-time --period daily --limit 480

Forbid DataSHIELD to the user ``demouser``, by granting a zero allowance:

.. code-block:: bash

  opal datashield-quota --opal https://opal-demo.obiba.org --user administrator --password password --add --type user --subject demouser --limit 0

Raise the limit of a quota to 5 hours, leaving its other properties as they are:

.. code-block:: bash

  opal datashield-quota --opal https://opal-demo.obiba.org --user administrator --password password --update --id 1 --limit 300

Suspend a quota, and reinstate it later:

.. code-block:: bash

  opal datashield-quota --opal https://opal-demo.obiba.org --user administrator --password password --update --id 1 --disabled
  opal datashield-quota --opal https://opal-demo.obiba.org --user administrator --password password --update --id 1 --enabled

Delete a quota (the subject becomes unlimited again, unless a broader quota still applies):

.. code-block:: bash

  opal datashield-quota --opal https://opal-demo.obiba.org --user administrator --password password --delete --id 1

Report, for each usage metric, what a user has consumed against the quota that applies to them:

.. code-block:: bash

  opal datashield-quota --opal https://opal-demo.obiba.org --user administrator --password password --usage --subject demouser --json

Report the usage of the current user (does not require administration permissions):

.. code-block:: bash

  opal datashield-quota --opal https://opal-demo.obiba.org --user demouser --password password --usage --json

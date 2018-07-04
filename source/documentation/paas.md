## How to manage our internal PaaS organisation

Reliability engineering uses the GOV.UK PaaS organisation `gds-tech-ops`.

### Managing users

All tech leads and technical architects in RE should be OrgManagers.  This means that your tech lead or technical architect should be able to add you to the PaaS organisation.  They should use the [GOV.UK PaaS admin tool](https://login.cloud.service.gov.uk/login).

### Managing spaces and quotas

We have an overall quota for the organisation.  You can see the name of the quota we're on by running `cf org gds-tech-ops` and see the details of the quota with `cf quota $NAME` -- for example, `cf quota small`.

If one team uses up the organisation quota, it stops other teams from being able to create apps.  Therefore, teams should ensure they work in spaces, and that each space has a space quota.  If a team hits the quota for their space, it won't block other teams.  This is particularly problematic with memory usage.

To create a space with a name of `log-pipeline`, a memory quota of 1 Gb and a routes quota of 5, an OrgManager can run the following commands:

- `cf create-space-quota log-pipeline -m 1g -r 5`
- `cf create-space log-pipeline -o gds-tech-ops -q log-pipeline`

To update the quota later, an OrgManager can run:

- `cf update-space-quota $NAME -m 2g` where `2g` is the new memory quota value

The command line accepts different units, such as `256m`, `512m`, `1g`, `5g`.

It's okay for a space and a space quota to have the same name as each other.

To list the existing space quotas for an organisation, run `cf space-quotas`.

[GOV.UK PaaS docs on adding users]: https://docs.cloud.service.gov.uk/#adding-users

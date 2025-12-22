## Overview

Exposures are a great way to create visibility on how your dbt models are being used downstream. Analytics workflow has been definitely been made easier using exposures. For example, there's a dashboard that is frequently look at that analyzes data from dbt Labs' training website - learn.getdbt.com. Because an exposure was configured for this dashboard, people were able to figure out which models and metrics were feeding into it. This is great because there had a few minor changes that were needed to make to a downstream model that the dashboard referenced, and the exposure lets someone know which person at dbt labs to reach out to, because this quickly let people know who to tag in their PRs.

Data management is challenging, and it's increasingly challenging the more data you have to keep track of. With exposures, you can clearly see which models and metrics feed into which exposures, and therefore, which dashboards. Exposures let you fully document your data ecosystem.

<img width="1182" height="524" alt="image" src="https://github.com/user-attachments/assets/aaaa95f3-3d90-465a-9d6e-2c97c2f570b9" />

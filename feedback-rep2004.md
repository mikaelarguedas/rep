## [ROS-Security] Feedback to REP-2004 Package quality categories

### General remarks

- How does a user consume the fact that a given package is in a given category without undue burden? Forcing the user to check a list maintained on a wiki requires them to have 100% knowledge of every dependency of every package that they may have just `apt install`ed. This could (and should) be scripted, but that still puts the onus of checking on the user. Could something similar to ubuntu’s repository components (main, restricted, universe…) be used? Then they actually need to opt-in to actually installing software of a given quality level.
- Lack of granularity in ‘quality level’
While having a few 'quality levels' is great to get a very quick overview of a package quality, it may also be misleading, masking the granularity of reality. A package that excels in all metrics but performs miserably in a single one (for any reason) may be ranked in one of the lower grades thus not encouraging its use. In reality the package may only need a little external help to get a full score.
An example of this is a package not available on one of the Tier1 platforms, thus not qualifying to be quality level < 4. But being production ready and complying with every other criterium to be level 1.
We think adding a full 'report card' could be useful to assess how a package is failing to meet criteria for the higher quality level. For this 'report card' to be useful, it should be quickly and easily readable. We could consider a 'spider chart' (or [radar chart as per wikipedia](https://en.wikipedia.org/wiki/Radar_chart)), or a table like [here](https://github.com/ros-infrastructure/rep/blob/c8bd456f531acc4863d0bb8888c28b10f9271492/rep-2004.rst#quality-level-comparison-chart).

### Security specific context and feedback

#### Quality Levels and the Vulnerability Disclosure Policy
The VDP tells the public we’d like a flat 90-day grace period between when we receive a vulnerability before it’s made public.  In the interest of keeping the VDP simple, I recommend keeping code quality out of this public-facing document.  We can--and should--strive to do better for high quality code, but I don’t believe that needs to be a part of this document.

#### Quality Levels and Vulnerability Remediation
Internally, however, we should set a higher standard for higher quality code.
Level 1 and 2 code will be widely deployed in the field. Fixes should be made available this code quickly to protect production robots.
Level 3 and some level 4 code may not be deployed in robots, but will be used daily by firms that build robots.  High risk vulnerabilities should be handled quickly to protect development environments.
CVSS is the defacto standard for risk assessing vulnerabilities.  Although flawed, it’s better than trying to create a new standard.

#### Remediation Timeline
Here’s an initial proposal on responsiveness based on the principles above.  This would be a commitment by the ROS 2 developer community.
Triage within 3 days for all reports, triage assigns a CVSS score and a maintainer to provide a fix
Maintainer is expected to provide a fix according to this timeline; the maintainer may also change the CVSS score as they dig into the issue:


|                   | High Risk<br> CVSS 9+ | Medium Risk<br> CVSS 6-9            | Low Risk<br>CVSS <6                       |
| ----------------- | --------- | ---------------------- | ------------------------------ |
| Quality Level 1   | 7 days    | 30 days                | No timeline, use issue         |
| Quality Level 2   | 7 days    | 30 days                | No timeline, use issue         |
| Quality Level 3   | 30 days   | No timeline, use issue | No timeline, use issue         |
| Quality Level 4-5 | 30 days   | No timeline, use issue | No timeline, use issue         |



Once the maintainer has approved the code update, the code is built and distributed according to the normal timeline.


## Suggestions outside of REP but linked to it:

- Consider providing tooling to help people evaluate / generate the quality level and files associated with quality level (could go from a simple list of Y/N questions to actually pulling info of all the dependencies etc)
- How does this connect with REP-2005 ? How would one go about filing vulnerabilities in e.g. Fast-RTPS?
- Provide recommendation on linters checking for quality / security issues (see https://github.com/ros-infrastructure/rep/pull/218#discussion_r370583550) (TODO by Security WG)

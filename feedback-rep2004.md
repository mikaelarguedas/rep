## [ROS-Security] Feedback to REP-2004 Package quality categories

The proposal looks great and we really like the goals of it.
The voluntary nature of it makes us wonder how to best incentivize people to pay close attention to the quality and security of their packages.
Based on this we compiled a list of questions/remarks to hopefully spark conversation on how things could be improved for a global buy-in.
Most would not fit in this REP as is but could help picture what the impact of the REP can be and what framework around it can drive ROS quality and security forward.

- incentive:
What is the incentive for a maintainer to aim to a high category ? Is there a clear benefit in being in a specific one ?
- accountability:
How to report that a package doesn't match the claimed quality level?
What is the process from there?
Why will package authors care? And if they don't, why will users find meaning in these categories?
- Accessibility:
  - How will use access and consume the quality levels information?
  - Repository components [were briefly mentioned](https://github.com/ros-infrastructure/rep/pull/218#discussion_r376734511) as one way to actually have a side effect of being in a given category (as it would directly relate to users opting into using packages of a given category). However, there is a desire not to mandate such things from this REP, which re-emphasizes the above point. Is the plan for the development guide or a further REP to build on this one?
- Granularity:
While having a few 'quality levels' is great to get a very quick overview of a package quality, it may also be misleading, masking the granularity of reality.
A package that excels in all metrics but performs miserably in a single one (for any reason) may be ranked in one of the lower grades thus not encouraging its use.
In reality the package may only need a little external help to get a full score.
An example of this is a package not available on one of the Tier1 platforms, thus not qualifying to be quality level < 4 while being production ready and complying with every other criterium to be level 1.
We think adding a full 'report card' could be useful to assess how a package is failing to meet criteria for the higher quality level.
For this 'report card' to be useful, it should be quickly and easily readable.
We could consider a 'spider chart' (or [radar chart as per wikipedia](https://en.wikipedia.org/wiki/Radar_chart)), or a table like [here](https://github.com/ros-infrastructure/rep/blob/c8bd456f531acc4863d0bb8888c28b10f9271492/rep-2004.rst#quality-level-comparison-chart).

- How to make declaring quality level less cumbersome:
  Consider providing tooling to help people evaluate / generate the quality level and files associated with quality level (could go from a simple list of Y/N questions to actually pulling quality levels of all dependencies etc)

- Non ROS packages:
  - How does this connect with REP-2005 ?
  - If a package listed in REP-2005 doesn't match quality criteria here, should it disqualify dependent from claiming that level?

- Tooling to increase adoption:
  - Consider providing tooling to help people generate the quality declaration files associated with quality level (could go from a simple list of Y/N questions to actually pulling info of all the dependencies etc)

- Criteria relevant for quality and security:
As mentionned by @vmayoral above, quality and security really play hand in hand and we should really strive to improve both for any ROS package intended to be used widely, especially those in or talking to deployed systems.
  - Provide minimum requirements for code quality based on analysis tools: This was mentioned earlier [here](https://github.com/ros-infrastructure/rep/pull/218#discussion_r370583550) It would be great to have a set of required linters for a specific level. It could be part of `ament_lint_common`, or a different set of linters only for "Level1". Inputs from the quality WG, tooling WG, TSC and other interested parties would be very valuable to converge on a set of tools + metrics.
  - Can maintainer responsiveness be taken into account for quality levels?
  An ability to fix and release vulnerabilities in a timely manner is something we find relevant when assessing the quality of a package in the long run
  - Fixing reported issues: The security WG has been working on putting together a Vulnerability Disclosure Policy document for ROS packages. The level of responsiveness to addressing vulnerabilities is in our opinion an important criteria for quality levels. Here is an example (quantitative this time)

|                   | Critical/High Risk<br> CVSS 7.0+ | Medium Risk<br> CVSS 4.0-6.9            | Low Risk<br>CVSS <3.9                       |
| ----------------- | --------- | ---------------------- | ------------------------------ |
| Quality Level 1   | 7 days    | 30 days                | No timeline, use issue         |
| Quality Level 2   | 7 days    | 30 days                | No timeline, use issue         |
| Quality Level 3   | 30 days   | No timeline, use issue | No timeline, use issue         |
| Quality Level 4-5 | No timeline, use issue   | No timeline, use issue | No timeline, use issue         |

Here we take an example of different expectations for fixing and releasing based on the quality level and the criticality of the issue.
While the scoring mechanism used and the timelines are up for discussion we'd like to know if such an approach could be considered for quality levels.

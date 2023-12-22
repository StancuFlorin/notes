---
title: "How to play HEVC/H.265 videos using Plex on Windows without transcoding"
date: 2023-12-21
---

Here is my guide on playing HEVC videos on Windows through Plex Web Player without the need for transcoding. Additionally, external .srt subtitle files are incorporated.

- Install [HEVC Video Extensions](https://apps.microsoft.com/detail/9NMZLZ57R3T7?hl=en-US&gl=US) from Microsoft Store. You will have to pay 1$ for it.
- Opt for Microsoft Edge; there's no need to fret as it's actually quite pleasant. It has become my primary browser. Over the past few months, I transitioned from Chrome to Brave, and now I exclusively use Edge.
- Install [h265ify](https://microsoftedge.microsoft.com/addons/detail/h265ify/hpamdcillfipbkdijibjoojnofelpgjb) Edge extension. No extra configuration is needed.
- Make sure you are using version `118` of Edge. I am curently using `Version 118.0.2088.122 (Official build) (64-bit)`.

![plex_playback_settings](/assets/img/posts/plex_playback_settings.png)

## How to downgrade Edge

It's likely that you don't have version 118 installed. If your version is lower than 118, consider avoiding the update. I encountered problems with HEVC video playback when using version 120 for a few days, prompting me to find a workaround by downgrading to version 118 and disabling updates. Unfortunately, Edge lacks a user-friendly method for disabling updates, but there is a solution.

### How to disable Edge updates

In the `Windows Services` application, deactivate the following three services by double-clicking on the service name and adjusting the startup type to `Disabled`.

![edge_windows_services](/assets/img/posts/edge_windows_services.png)

In the `Task Scheduler` application, deactivate the following three tasks by right-clicking on the task name and choose `Disable`.

![edge_task_scheduler](/assets/img/posts/edge_task_scheduler.png)

### How to downgrade Edge

When reverting to a previous version of Edge, start by downloading the most recent build for version 118 from the official [Microsoft website](https://www.microsoft.com/en-us/edge/business/download?form=MA13FJ).

To revert to a previous version, simply execute the following command in your terminal. Although you won't observe any progress, after a few minutes, an Edge shortcut will be created on your Desktop, indicating a successful downgrade. Before opening Edge, ensure that the disabled services and tasks remain deactivated.

```
msiexec /I MicrosoftEdgeEnterpriseX64.msi /qn ALLOWDOWNGRADE=1
```

With the older version of Edge in use, prevent any updates. You may receive frequent prompts to install new updates when accessing the settings page. Simply refrain from allowing the `Microsoft Edge Update` application to initiate.

This is the information you should find on the `Settings > About Microsoft Edge` page.

![edge_updates_disabled](/assets/img/posts/edge_updates_disabled.png)

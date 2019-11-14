---
tags: [Notebooks/itblog]
title: Disown job
created: '2019-09-29T11:18:04.461Z'
modified: '2019-10-18T14:22:56.221Z'
---

Every so often I fire up and job and then need to end my ssh session for one reason or another. Until the other day I did not realise that you could leave an already existing process running (other than using screen or nohup).

Use disown.

Run your job.

CTRL+Z to stop the job.

To put it in the backgroud.  
`$ bg`  
Then to disown.  
`$ disown -h`

Now logout (CTRL+D) and it will just keep on running!

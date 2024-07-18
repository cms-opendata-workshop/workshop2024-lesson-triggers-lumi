---
title: Setup
---

:::::::::::: prereq

For this lesson you will need a new container for the `brilcalc` tool to calculate luminosities and some trigger information. **Please install the brilcalc container**:

```bash
docker run -it --name brilws gitlab-registry.cern.ch/cms-cloud/brilws-docker
```

If you are working with apptainer on a remote cluster, you can try the [conda installation instructions](https://opendata.cern.ch/docs/cms-guide-luminosity-calculation) for brilcalc.
(Note: if you are a young student working on a remote cluster, feel free to just follow along -- this is a tool that is important for research-level open data use, but not for educational use.)

::::::::::::
---
title: LFX Mentorship Summer'23
date: 2023-10-17
tags: [kubearmor, journey]
---

I had completed my LFX Mentorship in KubeArmor project. This is a
pending report of my work and write-up about my journey.

# KubeArmor Work

This is a three month long mentorship program where you work on one or
more issues or features of the project. My primary goal was to support
the OCI registry and OCI hooks in KubeArmor as outlined in [this
GitHub
issue](https://github.com/kubearmor/KubeArmor/issues/1130). There are
two major tasks that need to be completed in 3 months. We planned to
spend 1 month on the OCI registry and 2 months for OCI hook support
because the former is easy compared to the latter. We used to have
weekly meeting each Tuesday 18:00 IST for sharing our progress and
general discussion.

I am thankful to my mentors Barun, Ankur, Rahul and Anurag for their
continuous guidance and support throughout. I documented both of my
work below.

# OCI Registry

Distributing and managing KubeArmor security policies would be very
convenient if it supports OCI registry. This new feature distributes
KubeArmor policies as OCI Artifacts using OCI registries. Users can
store policies side by side with container images.

KubeArmor CLI tool - `karmor`, supports interacting with any
registries that are OCI compliant. It can push any valid KubeArmor
policy to the registry, and also pull it locally for use. Few sample
karmor oci commands that interact with registry are shown below:

```
// Push mypolicy.yaml to local registry localhost:5000
$ karmor oci push -i localhost:5000/myimage:latest -f mypolicy.yaml

// Push example-policy.yaml to docker registry. Already login to docker registry using docker login command
$ karmor oci push -i docker.io/user/repo:v1 -f example-policy.yaml

// Pull already pushed policy from registry to output directory.
$ karmor oci pull -i docker.io/user/repo:v1 -o /path/to/output
```

To authenticate with registries (eg. Docker registry) store user
credentials to the local store by running `docker login` command. The
karmor oci command uses local credentials automatically for
authentication. Karmor oci also accepts username and password for
authentication via –username and –password flags.

Set "KARMOR_OCI_TLS_INSECURE=true" environment variable for connecting
to registry via HTTP instead of HTTPS.

Run `karmor oci -h` command to know available options and usages.

# OCI Hooks

KubeArmor currently mounts container runtime unix domain sockets
inside a container. Exposing the CRI socket is considered
dangerous. Allowing access to sockets gives full control on container
management. It means you can abruptly create or delete
containers. Mounting CRI sockets in containers can lead to security
issues and hence people avoid it. Some policy enforcers detect and
disallow mounting container sockets.

This is a proposal to use OCI hooks instead of mounting runtime
sockets for listening to container events.

The design proposal and OCI hooks setup for different container
runtimes are shared on [KubeArmor
wiki](https://github.com/kubearmor/KubeArmor/wiki/KubeArmor-OCI-Hooks-Design)
and progress tracked separately
(here)[https://github.com/kubearmor/KubeArmor/issues/1390].

# Challenges Faced

For OCI hooks implementations, there are different container runtimes
such as crio-o, docker, containerd. Some runtimes support configuring
hooks, but other don't support it. For example OCI hook is not
implemented for Docker. So we have tried local clusters with different
container runtimes and set up OCI hooks on it.

Before finalizing OCI hooks we have explored other options that could
eliminate the need of mounting sockets such as k8s pod informers,
linux fanotify, containerd NRI. We compared these alternatives to see
which one fits for our use case.

# Final Thoughts

The mentorship program helped me to think through the real problem and
solve it with the guidance of the team. OCI registry support will be
ready for public use after PR gets accepted. OCI hooks need further
analysis and implementation. I felt very welcomed and fun working with
the KubeArmor team.


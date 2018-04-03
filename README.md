# CPU affinity test for resin multicontainer

An example project running demonstrating CPU affinity, keeping one of the
system CPUs for one of the services alone, in a multi-container environment.
The demo code assumes a 4-core environment, such as a Raspberry Pi 3, but it can
be easily adjusted

*   `idle`: the "priority" project, of just idling. Assigned for CPU 0.
*   `busy`: the "background" project that normally eats up resources, in this case [`stress`](https://linux.die.net/man/1/stress) running on the remaining 1-3 cores, as a 10-worker process, clearly saturating the available CPU resources.

Deploy this on a resin.io device, and check that core 0 is pretty much idle (might share some of the system resources, but not with the `busy` task). See this by either:

*   connect to the Host OS, and run `top` to see the percentage usage (should be ~75% busy, ~25% idle in a 4-core device), or
*   connect to the `idle` service, and run `htop` to have a graphical view of the system being used.

To see how things behave, when CPU affinity is disabled, comment out or delete the `cpuset` lines in `docker-compose.yml`.

## License

Copyright 2018 Resinio Ltd.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

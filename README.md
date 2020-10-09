<!--
  Licensed to the Apache Software Foundation (ASF) under one or more
  contributor license agreements.  See the NOTICE file distributed with
  this work for additional information regarding copyright ownership.
  The ASF licenses this file to You under the Apache License, Version 2.0
  (the "License"); you may not use this file except in compliance with
  the License.  You may obtain a copy of the License at

      http://www.apache.org/licenses/LICENSE-2.0

  Unless required by applicable law or agreed to in writing, software
  distributed under the License is distributed on an "AS IS" BASIS,
  WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
  See the License for the specific language governing permissions and
  limitations under the License.
-->

# Apache Yetus test-patch

This action enables Apache Yetus' change testing facilities via GitHub actions
without significant configuration. For simple usage (with bleeding edge versions),
add the following work flow:

```yaml
---
name: Apache Yetus

on: [push, pull_request]  # yamllint disable-line rule:truthy

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
      - name: checkout
        uses: actions/checkout@v2
        with:
          path: src
          fetch-depth: 0
      - name: Apache Yetus test-patch
        uses: apache/yetus-test-patch-action@main
        with:
          basedir: ./src
          patchdir: ./out
          buildtool: nobuild
          githubtoken: ${{ secrets.GITHUB_TOKEN }}
      - name: Artifact output
        if: ${{ always() }}
        uses: actions/upload-artifact@v2
        with:
          name: apacheyetuspatchdir
          path: ${{ github.workspace }}/out
```

For more complex usage or just more information in general, see the
[Apache Yetus Website](https://yetus.apache.org/documentation/in-progress/precommit/robots/githubactions/).

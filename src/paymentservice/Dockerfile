# Copyright 2020 Google LLC
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

FROM node:16-alpine AS base

FROM base AS builder

WORKDIR /usr/src/app/

COPY ./src/paymentservice/package.json ./

RUN npm install --only=production

# -----------------------------------------------------------------------------

FROM base

WORKDIR /usr/src/app/

COPY --from=builder /usr/src/app/node_modules/ ./node_modules/
COPY ./src/paymentservice/ ./
COPY ./pb/ ./proto/

EXPOSE ${PAYMENT_SERVICE_PORT}
ENTRYPOINT [ "node", "--require", "./tracing.js", "./index.js" ]

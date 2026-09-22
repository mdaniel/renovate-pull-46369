# Currently

- buf.yaml has a very old sha-pinned reference `buf.build/protocolbuffers/wellknowntypes:ba48c1a6dc7d47d0aa9940aa3601b039`
- buf.gen.yaml has several kinds of references in it:
  - `remote: buf.build/protocolbuffers/go:v1.36.6`
  - `remote: buf.build/grpc-ecosystem/gateway:v1.0.0` which is a valid-looking label but does not exist
  - `remote: buf.build/grpc/go:v1` which is malformed from buf's point of view, but leaves it intact since there is not v2
  - `remote: buf.build/connectrpc/gosimple` which is versionless, and thus we will skip it to allow it to continue to be versionless
- buf.gen.rust.yaml is a simple version bump but in a non-default language filename


# The Run

```bash
read -s -p 'gh token? ' RENOVATE_TOKEN
export RENOVATE_TOKEN

read -s -p 'buf token? ' BUF_TOKEN
export BUF_TOKEN

cat >config-46369.js <<"JS"
const hostRules = [];
if (process.env.BUF_TOKEN) {
  hostRules.push({
    hostType: 'buf-plugin',
    matchHost: 'buf.build',
    token: process.env.BUF_TOKEN,
  });
  hostRules.push({
    hostType: 'buf-module',
    matchHost: 'buf.build',
    token: process.env.BUF_TOKEN,
  });
}

export default {
  dryRun: 'full',
  binarySource: 'docker',

  // Pin the buf version containerbase installs (omit for latest).
  constraints: { buf: '1.72.0' },

  // Focus the run on just this feature; no npm/docker/etc
  enabledManagers: ['buf'],

  hostRules,
};
JS
LOG_LEVEL=debug \
RENOVATE_CONFIG_FILE="${PWD}/config-46369.js" \
  pnpm start mdaniel/renovate-pull-46369
```

# Its opinion

```json
{
  "config": {
    "buf": [
      {
        "deps": [
          {
            "depName": "protocolbuffers/go",
            "datasource": "buf-plugin",
            "registryUrls": ["https://buf.build"],
            "currentValue": "v1.36.6",
            "replaceString": "buf.build/protocolbuffers/go:v1.36.6",
            "autoReplaceStringTemplate": "buf.build/protocolbuffers/go:{{#if newValue}}{{newValue}}{{/if}}",
            "updates": [
              {
                "bucket": "non-major",
                "newVersion": "v1.36.12",
                "newValue": "v1.36.12",
                "newMajor": 1,
                "newMinor": 36,
                "newPatch": 12,
                "updateType": "patch",
                "isBreaking": false,
                "branchName": "renovate/protocolbuffers-go-1.x"
              }
            ],
            "packageName": "protocolbuffers/go",
            "versioning": "semver-coerced",
            "warnings": [],
            "sourceUrl": "https://github.com/protocolbuffers/protobuf-go",
            "registryUrl": "https://buf.build",
            "homepage": "https://buf.build/protocolbuffers/go",
            "currentVersion": "v1.36.6",
            "isSingleVersion": true,
            "fixedVersion": "v1.36.6"
          },
          {
            "depName": "grpc-ecosystem/gateway",
            "datasource": "buf-plugin",
            "registryUrls": ["https://buf.build"],
            "currentValue": "v1.0.0",
            "replaceString": "buf.build/grpc-ecosystem/gateway:v1.0.0",
            "autoReplaceStringTemplate": "buf.build/grpc-ecosystem/gateway:{{#if newValue}}{{newValue}}{{/if}}",
            "updates": [
              {
                "bucket": "major",
                "newVersion": "v2.30.0",
                "newValue": "v2.30.0",
                "newMajor": 2,
                "newMinor": 30,
                "newPatch": 0,
                "updateType": "major",
                "isBreaking": true,
                "branchName": "renovate/grpc-ecosystem-gateway-2.x"
              }
            ],
            "packageName": "grpc-ecosystem/gateway",
            "versioning": "semver-coerced",
            "warnings": [],
            "sourceUrl": "https://github.com/grpc-ecosystem/grpc-gateway",
            "registryUrl": "https://buf.build",
            "homepage": "https://buf.build/grpc-ecosystem/gateway",
            "currentVersion": "v1.0.0",
            "isSingleVersion": true,
            "fixedVersion": "v1.0.0"
          },
          {
            "depName": "grpc/go",
            "datasource": "buf-plugin",
            "registryUrls": ["https://buf.build"],
            "currentValue": "v1",
            "replaceString": "buf.build/grpc/go:v1",
            "autoReplaceStringTemplate": "buf.build/grpc/go:{{#if newValue}}{{newValue}}{{/if}}",
            "updates": [],
            "packageName": "grpc/go",
            "versioning": "semver-coerced",
            "warnings": [],
            "sourceUrl": "https://github.com/grpc/grpc-go",
            "registryUrl": "https://buf.build",
            "homepage": "https://buf.build/grpc/go",
            "currentVersion": "v1.6.2",
            "fixedVersion": "v1"
          },
          {
            "depName": "connectrpc/gosimple",
            "datasource": "buf-plugin",
            "registryUrls": ["https://buf.build"],
            "skipReason": "unspecified-version",
            "updates": [],
            "packageName": "connectrpc/gosimple"
          }
        ],
        "packageFile": "buf.gen.yaml"
      },
      {
        "deps": [
          {
            "depName": "protocolbuffers/wellknowntypes",
            "datasource": "buf-module",
            "registryUrls": ["https://buf.build"],
            "currentDigest": "ba48c1a6dc7d47d0aa9940aa3601b039",
            "updates": [
              {
                "updateType": "digest",
                "newDigest": "f1151727eddb493abf82a1d919dc35e4",
                "branchName": "renovate/protocolbuffers-wellknowntypes-digest"
              }
            ],
            "packageName": "protocolbuffers/wellknowntypes",
            "versioning": "loose",
            "warnings": []
          }
        ],
        "packageFile": "buf.lock"
      }
    ]
  }
}
```

FROM hadolint/hadolint:v2.12.0-alpine@sha256:3c206a451cec6d486367e758645269fd7d696c5ccb6ff59d8b03b0e45268a199 AS dockerfile-lint
FROM koalaman/shellcheck:v0.11.0@sha256:61862eba1fcf09a484ebcc6feea46f1782532571a34ed51fedf90dd25f925a8d AS shellcheck

FROM mcr.microsoft.com/devcontainers/javascript-node:1-22@sha256:0d29e5fdc64f8397cd502223e0c4679f1e60877ca0fd2db4f2e2e0028e4271af

COPY --from=dockerfile-lint /bin/hadolint /usr/bin/hadolint

COPY --from=shellcheck /bin/shellcheck /usr/bin/

# hadolint ignore=DL3008
RUN apt-get update && apt-get install -y --no-install-recommends \
        pre-commit \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

FROM hadolint/hadolint:v2.15.1-alpine@sha256:a1d49ae1a4e83c1dbad26b8c1ad7588c8bd1e04f4866b34ad3cac50335198552 AS dockerfile-lint
FROM koalaman/shellcheck:v0.11.0@sha256:61862eba1fcf09a484ebcc6feea46f1782532571a34ed51fedf90dd25f925a8d AS shellcheck

FROM mcr.microsoft.com/devcontainers/javascript-node:5-22@sha256:2dffe9cdd928c3ebf074fb47b6a37df7934d090df160fae46aa4eb36780942ea

COPY --from=dockerfile-lint /bin/hadolint /usr/bin/hadolint

COPY --from=shellcheck /bin/shellcheck /usr/bin/

# hadolint ignore=DL3008
RUN apt-get update && apt-get install -y --no-install-recommends \
        pre-commit \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

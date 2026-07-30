FROM hadolint/hadolint:v2.15.0-alpine@sha256:ddabce597257a5b466cc60878090de88b0fd191b84eb7652bddfe88ad192d0d5 AS dockerfile-lint
FROM koalaman/shellcheck:v0.11.0@sha256:61862eba1fcf09a484ebcc6feea46f1782532571a34ed51fedf90dd25f925a8d AS shellcheck

FROM mcr.microsoft.com/devcontainers/javascript-node:4-22@sha256:aac847b276570cac53f0fef23733793a38190e655cecd7b74c5cac7816b6ff53

COPY --from=dockerfile-lint /bin/hadolint /usr/bin/hadolint

COPY --from=shellcheck /bin/shellcheck /usr/bin/

# hadolint ignore=DL3008
RUN apt-get update && apt-get install -y --no-install-recommends \
        pre-commit \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

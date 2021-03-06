# Release Process

1. Review and discuss any potential modifications to the [support matrix/policy][support-policy]
2. Create a draft release in github
3. Tag the repository and push the tag
   - An [OWNER](/OWNERS) runs `git tag -s $VERSION` and inserts the changelog and pushes the tag with `git push $VERSION`
4. Run `make release-binaries`
5. Attach the tarball to the drafted release
6. Attach `clusterctl` to the drafted release (for darwin and linux architectures)
7. Write the [release notes](#release-notes)
8. Build and push the container image
9. Publish release
10. Announce the release

## Versioning

cluster-api-provider-azure follows the [semantic versionining][semver] specification.

As of this writing, we have not produced as a major or minor release. 

Current pre-release versions can be expected to have breaking changes as we move towards declaring a public API version.

Example versions:
- Pre-release: `v0.1.0-alpha.4`
- Minor release: `v0.1.0`
- Patch release: `v0.1.1`
- Major release: `v1.0.0`

## Expected artifacts

1. A container image containing the azure-provider manager binary
2. A release tarball containing the manifest-templates and a script to generate        the actual manifests
3. `clusterctl`
4. Release notes

## Output locations

### Container image

The container image will live in the registry `quay.io/k8s/cluster-api-provider-azure`
under the image name `cluster-api-azure-controller:<tag>` where `<tag>` is
replaced by the version being released.

### Manifests

Manifests must be generated by hand.

Running `make release-binaries` will create a tarball that you can attach to
the drafted release.

### Binaries

The binary produced by a release is the `clusterctl` binary. There should be support for both darwin and linux architectures.

### Release Notes

Release notes are written by hand using the [release notes template][template] as a guide.

Generally, we'll make a [HackMD](https://hackmd.io/) and share the release note
 responsibility for a few days in advance of the release.

The markdown is shared in the Kubernetes slack in the channel #cluster-api-azure.

## Communication

### Pre-releases

1. Announce the release in Kubernetes Slack on the #cluster-api-azure channel.

### Official releases

1. Follow the communications process for [pre-releases](#pre-releases)
2. An announcement email is sent to `kubernetes-sig-azure@googlegroups.com` and `kubernetes-sig-cluster-lifecycle@googlegroups.com` with the subject `[ANNOUNCE] cluster-api-provider-azure $VERSION is released`


[semver]: https://semver.org/#semantic-versioning-200
[support-policy]: /README.md#support-policy
[template]: /docs/release-notes-template.md

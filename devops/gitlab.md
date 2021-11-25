# gitlab and dependency proxy

you can configure a dependency proxy to avoid dockerhub limits

for exemple you can use your group dependency proxy : ``gitlab.com/groups/37rtm/dependency_proxy/containers``
to configure you docker daemon ``/etc/docker/daemon.json``

````json
{
        "exec-opts": ["native.cgroupdriver=systemd"],
        "registry-mirrors": ["https://gitlab.com/groups/37rtm/dependency_proxy/containers"]
}
````

## References

- <https://stackoverflow.com/questions/33054369/how-to-change-the-default-docker-registry-from-docker-io-to-my-private-registry>

## HAPROXY Ingress Test

This configuration can be used to set up a test cluster to verify use of the
[HAPROXY Ingress Controller] for Rate Limiting.


[HAPROXY Ingress Controller]: https://www.haproxy.com/documentation/kubernetes/latest/

### Set Up

1. Create a test project with a Kubernetes cluster
2. Apply all of the yaml files
3. Use `kubectl get services -A` to get the external IP of the ingress-controller
4. Test using `curl -v [ip]:80/echo` ten times, confirming 200 response each time
5. Confirm 403 on the eleventh attempt

### Configuration Details

1. The echo ingress is set up to limit rate on [http-request]
2. The echo ingress specifies haproxy in *ingressClassName*
3. The haproxy-ingress file contains an IngressClass that binds the *ingressClassName* to the ingress controller

Note that the haproxy-ingress file is mostly identical to the one in the
[installation documentation] under "Install with kubectl".

[http-request]: https://cbonte.github.io/haproxy-dconv/1.9/configuration.html#4.2-http-request
[installation documentation]: https://www.haproxy.com/documentation/kubernetes/latest/installation/community/google/

### Rate Limiting Details

For detail on the rate limiting, search for *stick-table* in the yaml files and
refer to the [Introduction to HAProxy Stick Tables].

The [Ingress Controller 1.5 announcement] gives additional detail on this
functionality.

[Introduction to HAProxy Stick Tables]: https://www.haproxy.com/blog/introduction-to-haproxy-stick-tables/
[Ingress Controller 1.5 announcement]: https://www.haproxy.com/blog/announcing-haproxy-kubernetes-ingress-controller-1-5/

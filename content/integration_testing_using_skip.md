+++
title = "You can use testing.Skip() instead of build tags for integration tests"
date = 2021-05-05

[taxonomies]
tags = ["golang", "testing"]
+++

A pattern I've seen often in Go is to use build tags for integration tests, so you could exclude them when running `go test` 

This works OK but has some pitfalls, especially around IDEs and other tooling which often does not lint or compile build tags unless explicity set, so compiler errors will not surface.

After reading [dont-use-build-tags-for-integration-tests](https://peter.bourgon.org/blog/2021/04/02/dont-use-build-tags-for-integration-tests.html) I've started to try using the `t.Skip()` instead with an environment variable.

For example: 

```go
func TestIntegration(t *testing.T) {
	integrationFlag := os.Getenv("INTEGRATION")
	if integrationFlag == "" {
		t.Skip("set INTEGRATION to run this test")
	}

	// ...
}
```


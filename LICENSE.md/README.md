# helm-common-tpl

A repo for experimenting with a common set of helm templates with a wide variety of supporting features.

## Why?

Helm doesn't quite have the level of abstraction I want for my microservice templates. It's ok but a common set of templates would be better.

Some functionality I want:

- A field in values.yml specifies a directory, whose contents are converted into a file configmap
- Configmap hashes on deployments to force redeploy
- optional 'init-job' which is not recreated if it already exists
- a method of specifying initcontainer templates
- a method of templating json values

## Python / Node

I would almost prefer to use python or node to helm, since it would be easier to have libraries of templating functions.

## Plan for now

For now I plan on creating a values.yml file as a way of feeling our what makes sense for helm common functionality.

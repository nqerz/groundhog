# Github action runner on EC(S|2)

It is also possible to use elastic cumputes to generate runner server on public cloud.

## Steps

- Prepare an VPC and its components such as NAT, SG and others.
- Define metadata/environment variables for actions.
- Build start up scripts for the server initializing.
- Create function/lambda to generate elastic cumputes server on public cloud.

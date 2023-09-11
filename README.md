# Punch

Punch card automation for my company

## Usage

```bash
# build binary
make

# punch command
./punch \
    In|Out \
    --username=USERNAME \
    --password=PASSWORD \
    --company=COMPANY
```

See [example.md](example/example.md) for example

## Development

To check if automation works, with browser and dev tools showing, you could create a go file in the root directory

```golang
package main

import "github.com/imfulee/punch/hr_system"

func main() {
    nueip := NUEIP{...} // Initialize a NUEIP instance
    nueip.Punch(PunchStatus.In) // Place a punch status, declared in hr_system/
}
```

Then run

```bash
go run . -rod=show,devtools
```

## Container

To build as a container, replace podman with docker if that's what you use.

```bash
make podman
```

To run the container, you might want to setup up a cron job

```text
0 9 * * 1-5 podman run --rm <punch-image-name> /app/punch --USERNAME=<username> --PASSWORD=<password> --COMPANY=<company>
0 17 * * 1-5 podman run --rm <punch-image-name> /app/punch --USERNAME=<username> --PASSWORD=<password> --COMPANY=<company>
```

and manually set the cron time of your work, image name, username etc. 

## Roadmap

Things that I would like to further develop

- Add check is user is on old website, and switch to the new one 
- Make sure `rod` uses the right orientation and screen size
- Some reporting mechanism that it doesn't work, possibly by sending email?
- Add CI to build container
- Write test to check if punch in works

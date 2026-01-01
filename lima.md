
## Instalar lima

```
brew update
brew install lima
lima --version
brew install lima-additional-guestagents

```

## crear maquina x86

```
limactl create --name=x86_emulation_vm

```


- Borrar lima
```
limactl delete --force $(limactl ls -q)
rm -rf ~/.lima
rm -rf ~/Library/Caches/lima
brew uninstall lima

```

## Crear virtual

```
limactl create --name=x86_emulation_vm

yaml
arch: x86_64
vmType: qemu
# ...
rosetta:
  enabled: false

```

## Iniciar

```
limactl start x86_emulation_vm

limactl shell x86_emulation_vm

uname -m

```
Passo 1: Verificar o espaço disponível no disco
---

Primeiro, verifique o espaço disponível no disco usando o comando `lsblk` ou `fdisk -l`.

```bash
lsblk
```

Passo 2: Redimensionar a partição
---

Desmontar a partição (se necessário):

Se a partição estiver montada, você precisará desmontá-la antes de redimensioná-la. Supondo que a partição que você deseja redimensionar seja `/dev/sda1`, use:

```bash
sudo umount /dev/sda1
```

Usar o `fdisk` ou parted para redimensionar a partição:

O fdisk é uma ferramenta comum para manipulação de partições. Vamos usá-lo para redimensionar a partição.

```bash
sudo fdisk /dev/sda
```

Dentro do `fdisk`, siga estes passos:

- Pressione `p` para listar as partições existentes.
- Anote o número da partição que deseja redimensionar.
- Pressione `d` e o número da partição para deletá-la (não se preocupe, os dados não serão perdidos).
- Pressione `n` para criar uma nova partição.
- Escolha `p` para uma partição primária e o número da partição que você deletou.
- Use o mesmo número inicial da partição antiga.
- Para o tamanho, use todo o espaço disponível.
- Pressione `w` para salvar as alterações e sair.

Passo 3: Redimensionar o sistema de arquivos
---

Após redimensionar a partição, você precisará redimensionar o sistema de arquivos para usar o novo espaço.

Verificar e redimensionar o sistema de arquivos:

Para sistemas de arquivos `ext2`, `ext3` e `ext4`, use o `resize2fs`.

```bash
sudo resize2fs /dev/sda1
```

Para outros tipos de sistemas de arquivos, use a ferramenta apropriada (por exemplo, `xfs_growfs` para `XFS`).

Passo 4: Montar a partição
---

Monte novamente a partição:

```bash
sudo mount /dev/sda1 /mnt
```

Passo 5: Verificar
---

Verifique se a partição foi redimensionada corretamente:

```bash
df -h
```

Se tudo estiver correto, a partição agora deve mostrar o novo tamanho.

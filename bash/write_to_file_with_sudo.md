As you know, you may write to file like this:

```bash
echo 'text' > file.txt
```

If you write to file (without writing rights) throught sudo

```bash
sudo tee /etc/resolver/dev >/dev/null <<EOF
nameserver 127.0.0.1
EOF
```
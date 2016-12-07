.center[Redox OS]

.center[Revamping security for the age of IoT]

.center[![](redox.svg)]

.center[David Teller / `Yoric`]


---

# Linuxen are a great OSes

But the Linux security model is designed for servers.

???

- Can you trust the kernel?
- Can you trust the userspace?
- Can you trust the users?
- Can you patch exploits?

---

# How can we do better?

- Make the kernel safer & more secure
- Make the userspace safer & more secure
- Make your device easier to upgrade

---

# Safer & more secure

## The kernel

- Kernel => µKernel
- C => Rust

## The userspace

- `chroot` => Namespaces
- uid, gid => Capabilities (WIP)

---

# Easier to upgrade

- Kernel => µKernel
- Clear runtime dependencies (WIP)

---

# Namespaces

FIXME: TODO

---

# Capabilities (WIP)

```rust
fn spy() {
  {
    // By default, we do *not* have access to this file.
    let investigate = File::open("file:users/potus/confidential.txt", ...)
      .unwrap_err();


    // ...but we may request it.
    let cap = File::dup_from(pid, "file:users/potus/*.txt:r")
      .unwrap();


    // ...with the access, we can now open the file.
    let jackpot = File::open_at(cap, "file:users/potus/confidential.txt")
      .unwrap();
    let mut data = String::new();
    jackpot.read_to_string(&mut data)
      .unwrap();
  }

  // From this point, the capability has been dropped.
}
```

---

.center[Demo time]

---

# That's all, folks

- Not a MoCo project (yet?)
- http://redox-os.org

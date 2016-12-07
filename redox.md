class: middle, center


Redox OS

Revamping OS security for the age of IoT

![](redox.svg)

David Teller (Yoric)


---

# Linuxen are a great OSes


- Can you trust the kernel?
- Can you trust the userspace?
- Can you trust the users?
- Can you patch exploits?

The answer is generally **yes**.

--

...**except** on IoT/smart devices.

---

class: middle

# How can we do better?

- Make the kernel safer & more secure.
- Make the userspace safer & more secure.
- Make your device easier to upgrade.

---

class: middle

# Safer & more secure

## The kernel

- Kernel => µKernel
- C => Rust

## The userspace

- `chroot` => Namespaces
- uid, gid => Capabilities (WIP)

---

class: middle

# Easier to upgrade

- Kernel => µKernel
- Drivers => Processes
- Clear runtime dependencies (WIP)

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

class: center, middle

Demo time

---

class: middle

# That's all, folks

- Not a MoCo project (yet?)
- http://redox-os.org (LiveCD available)

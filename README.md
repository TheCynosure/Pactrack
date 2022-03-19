# Pactrack

Track local dependency installs like in pyenv and then remove them when done experimenting.


Don't consume if you want a real pacman wrapper. I use this locally to help with prototyping but its definitely not stable or bug-free.


### How it works

Pactrack is super basic but aims to solve the problem I have on Arch. I have no way to tell what I installed when I was messing around with prototyping and what I installed for actual use elsewhere. Pactrack aims to solve that by being a small pacman wrapper.

Everytime you install something through pacman, pactrack records that to the closest (using find-up) `.pactrack` file. Then if you remove it through pacman it also removes it from the `.pactrack` file. Simple enough. This lets you use pactrack just like pacman only when you are done with a project, all the dependencies that are still present on your system are in the local `.pactrack` file. To remove all of these simply issue a `pactrack remove_all` and they all will be deleted. Better yet they won't be deleted from the `.pactrack` file so you can install them all again. Its almost like a mini project-local pacman, but simplified to only the functionality I care about.

### To use:

To install:
```
./install
```

To use pactrack, in the root of the folder you want to track do:

```
touch .pactrack
```

And then to add dependencies use pactrack just like pacman:

```
pactrack -S clang
```

And then if during experimenting you find you want to no longer have that dependency:

```
pactrack -R clang
```

Finally, after all is done to remove everything leftover.

```
pactrack remove_all
```

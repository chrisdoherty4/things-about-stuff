# Handling slices of interfaces

>  An interface can store either a struct directly or a pointer to a struct. In the latter case, you still just use the interface directly, not a pointer to the interface.

Essentially, when you have a slice of interfaces don't try to specify that they are pointers as the 
interface can be both. Instead, just specify the interface as if by value.

```
type Thing interface {
    DoIt()
}

type Impl struct{}

func (t Impl) DoIt() {
    fmt.Println("Doing it")
}

func Execute(t Thing) {
    t.DoIt()
}

func main() {
    imp1 := Impl{}
    imp2 := &Impl{} // Pointer typoe

    // The execute function doesn't care.
    Execute(imp1)
    Execute(imp2)
}
```

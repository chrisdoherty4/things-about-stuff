# Variadic argument expansion

When a function declares an interface that takes a variadic argument, take note of the type.

    func Println(...interface{})

This can subsequently be called by 'expanding' a slice. However, that slice must be of type `[]interface{}`. `interface{}` has a specific memory layout so attempting to use anything else results in compilation error.

    s := []string{"hello", "world"}
    fmt.Println(, s...) // Compilation error


    s := make([]interface{}, 2)
    s[0] = "hello"
    s[1] = "world"
    fmt.Println(s...) // Fine

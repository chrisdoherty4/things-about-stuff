# Memory Leaks

If you have a C API call that returns a pointer to some managed memory SWIG
will attempt to copy that memory to a newly allocated piece of memory by default.
This results in a memory leak when there is a corresponding `free` style call
to the original C API call.

## Example memory leak

```
%module leek

%inline %{
const char * DoAThing();
void ReleaseAThing(const char * thing);
%}
```

```c
static _gostring_ Swig_AllocateString(const char *p, size_t l) {
  _gostring_ ret;
  ret.p = (char*)malloc(l);
  memcpy(ret.p, p, l);
  ret.n = l;
  return ret;
}

_gostring_ _wrap_DoAThing_leek_35b3bb0eb64a10f9() {
  char *result = 0 ;
  _gostring_ _swig_go_result;
  
  // Result points to some memory allocated by DoAThing()
  result = (char *)DoAThing();

  // Swig_AllocateString copies returned value to a _gostring_.
  _swig_go_result = Swig_AllocateString((char*)result, result ? strlen((char*)result) : 0); 

  // We haven't released the memory allocated by DoAThing()... 

  return _swig_go_result;
}


```

```c
const char * DoAThing();
void FreeAThing(const char *thing);
```

## Patching

You can patch the memory leak using a [typemap](http://www.swig.org/Doc4.0/Typemaps.html#Typemaps).

```
%module leek

typemap(ret) const char *
%{  
    FreeAThing($1);
%}

%inline %{
const char * DoAThing();
void ReleaseAThing(const char * thing);
%}
```

```c
_gostring_ _wrap_DoAThing_leek_6a93ceff5194347e() {
  char *result = 0 ;
  _gostring_ _swig_go_result;
  
  
  result = (char *)DoAThing();
  _swig_go_result = Swig_AllocateString((char*)result, result ? strlen((char*)result) : 0); 
  
  ReleaseAThing(result);
  
  return _swig_go_result;
}
```

# CODETAGS (ETIQUETAS DE CÓDIGO)

Programmers widely use ad-hoc code comment markup conventions to serve as reminders of sections of code that need closer inspection or review.
These codetags may show up in application code, unit tests, scripts, general documentation, or wherever suitable.


## CODETAGS LIST (LISTA DE ETIQUETAS DE CÓDIGO)
- NOTE
- OPTIMIZE
- TODO:    indicates that it must be completed.
- HACK
- XXX:     indicates that although the task has been completed it still needs to be optimized
- FIXME:   indicates problem that needs to be processed
- BUG

## EXAMPLES
```go
func CreateUniversity(name string) error {
    log.Printf("[CreateUniversity]")
    // TODO: code me
}
```


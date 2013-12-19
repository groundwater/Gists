

```
-B	brace expansion	Enable brace expansion (default setting = on)
+B	brace expansion	Disable brace expansion
-C	noclobber	Prevent overwriting of files by redirection (may be overridden by >|)
-D	(none)	List double-quoted strings prefixed by $, but do not execute commands in script
-a	allexport	Export all defined variables
-b	notify	Notify when jobs running in background terminate (not of much use in a script)
-c ...	(none)	Read commands from ...
checkjobs	 	Informs user of any open jobs upon shell exit. Introduced in version 4 of Bash, and still "experimental." Usage: shopt -s checkjobs (Caution: may hang!)
-e	errexit	Abort script at first error, when a command exits with non-zero status (except in until or while loops, if-tests, list constructs)
-f	noglob	Filename expansion (globbing) disabled
globstar	globbing star-match	Enables the ** globbing operator (version 4+ of Bash). Usage: shopt -s globstar
-i	interactive	Script runs in interactive mode
-n	noexec	Read commands in script, but do not execute them (syntax check)
-o Option-Name	(none)	Invoke the Option-Name option
-o posix	POSIX	Change the behavior of Bash, or invoked script, to conform to POSIX standard.
-o pipefail	pipe failure	Causes a pipeline to return the exit status of the last command in the pipe that returned a non-zero return value.
-p	privileged	Script runs as "suid" (caution!)
-r	restricted	Script runs in restricted mode (see Chapter 22).
-s	stdin	Read commands from stdin
-t	(none)	Exit after first command
-u	nounset	Attempt to use undefined variable outputs error message, and forces an exit
-v	verbose	Print each command to stdout before executing it
-x	xtrace	Similar to -v, but expands commands
-	(none)	End of options flag. All other arguments are positional parameters.
--	(none)	Unset positional parameters. If arguments given (-- arg1 arg2), positional parameters set to arguments.
```

# References

- http://tldp.org/LDP/abs/html/options.html

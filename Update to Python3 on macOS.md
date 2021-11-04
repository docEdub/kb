- Install `pyenv` command with homebrew
	```
	brew install pyenv
	```

- Install `python 3.10.0` with `pyenv`
	```
	pyenv install 3.10.0
	```

- to put Python 3 on the PATH before the system Python 3, change `~/.zshrc` to something like...
	```
	################################################################################### Command pyenv environment config.
	# See https://github.com/pyenv/pyenv/issues/1446#issuecomment-552040631

	# Clears every item in path
	unset path

	# List all path entries you want before the "standard" PATH
	PATH="\
	$HOME/.cargo/bin:\
	$HOME/.pyenv/versions/3.10.0/bin:\
	$HOME/lib/sbcl/bin:
	/usr/local/opt/openssl/bin:\
	/usr/local/opt/curl/bin:\
	/usr/local/opt/texinfo/bin:\
	/usr/local/opt/sqlite/bin:\
	/opt/homebrew/bin/"

	# Add the default directories AFTER the above (+=)
	PATH+=":/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/Library/Apple/usr/bin:\
	/Library/Apple/bin:/usr/libexec"

	# Now run the stuff that modifies the first entries in path
	# AMF: This doesn't seem to do anything so I added the Python 3.10.0 path above ^^^.
	# eval "$(pyenv init -)"

	# Clean up possible duplicates in path (ex. if iTerm is launching shells as login shells)
	# Make PATH Entries Great Again: (Unique)
	typeset -aU path

	# Finally, export the whole enchilada
	export PATH

	# Also make sure macOS gets the man pages right:
	export MANPATH=$(manpath)

	################################################################################### Nix build system config.
	export NVM_DIR="$HOME/.nvm"
	[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
	[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
	if [ -e /Users/andy/.nix-profile/etc/profile.d/nix.sh ]; then . /Users/andy/.nix-profile/etc/profile.d/nix.sh; fi # added by Nix installer
	```

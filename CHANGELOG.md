pyHIBP Changelog
================
v3.0.0 (2018-11-10)
-------------------
- **Backwards Incompatible Change**: The package name has been changed to fall in-line with the PEP 8 guideline calling for [all lowercase characters in package/module names](https://www.python.org/dev/peps/pep-0008/#package-and-module-names). Existing code will need to change invocations of ``pyHIBP`` to ``pyhibp``.
  - We will, however, still refer to the package/module as _pyHIBP_ when it is used outside of the context of Python code.
- **Future Python 2 Deprecation**: As per PEP 373, [Python 2.7.x support ends on 2020-01-01](https://www.python.org/dev/peps/pep-0373/#maintenance-releases). That being said, we will be dropping Python 2 as a supported version _prior_ to this date.
- The `requests` dependency has been bumped to require versions at or above `2.20.0` (due to CVE-2018-18074 affecting the `requests` package for older versions).

v2.1.1 (2018-09-18)
-------------------
- Bug fix: Corrected the capitalization of UA header, which was causing the majority of calls to ``get_account_breaches()`` to fail.

v2.1.0 (2018-07-21)
------------------
- **FUNCTION MOVED**: ``is_password_breached()`` has been fully removed from the core ``pyhibp`` module. It may be accessed
  from the ``pwnedpasswords`` module.
- Quasi-internal change: Relocated the GitLab repository to be in a group with the Jupyter Notebooks examples
  providing an interactive usage example.

v2.0.2 (2018-04-14)
-------------------
- **Final deprecation warning**: The ``pyhibp.is_password_breached`` shim will be removed in a future release. This
  function has been moved to the ``pwnedpasswords`` module, via ``from pyhibp import pwnedpasswords``.
- Internal: Shifts requirements/requirements.txt into setup.py, as as pip>=10 explicitly internalizes the method previously used
  to fill the install_requires variable.
- Internal: Removes vcversioner as a build requirement, opting to define the version in __version__.py.

v2.0.1 (2018-03-09)
-------------------
- **Deprecation warning**: The function ``is_password_breached`` has moved from ``pyhibp`` to the module named ``pwnedpasswords``. A wrapper has
  been left to ease transition to the new function; access via ``from pyhibp import pwnedpasswords``.
- The Pwned Passwords API version 2 has been released, and as such the following changes were made:
- ``is_password_breached`` no longer transmits the full SHA-1 hash to the Pwned Passwords API endpoint. This means any
  password that we want to check--such as a user's signup password--is secure. This is accomplished by transmitting
  the first 5 characters of the SHA-1 hash, and parsing the resultant list of partial SHA hashes for a match to the
  supplied password, or SHA-1 hash.
- The behavior of the prior ``is_password_breached()`` as implemented in v2.0.0 which submitted the full SHA-1 hash
  was dropped for added security.
- In addition to ``password`` and ``sha1_hash``, ``pwnedpasswords.is_password_breached()`` now accepts ``first_5_hash_chars``.
  This is to be set to the first five characters of a SHA-1 hash, and will return a list of partial hashes, along with
  the number of times the hash value in question was found in the Pwned Passwords corpus. This could be useful if you
  wish to perform verification of the hashes in the application importing this module.
- If ``password`` or ``sha1_hash`` is provided, the return value will now be an integer, corresponding to the number
  of times that password was located in the Pwned Passwords corpus, as per above. Integer zero (0) is returned if there
  was no match located, so one can still execute a call in the manner of ``if pw.is_password_breached():``.
- Unrelated to the code changes, the Pwned Passwords API (i.e, ``is_password_breached``) is no longer rate-limited.
  For more information, please see Troy Hunt's [post announcing Pwned Passwords v2](https://www.troyhunt.com/ive-just-launched-pwned-passwords-version-2/).


v2.0.0 (2018-02-01)
-------------------
- Initial release.

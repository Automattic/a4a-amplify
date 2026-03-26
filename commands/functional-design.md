If $ARGUMENTS is empty or does not contain a URL, ask the user to provide one before proceeding. Do not begin testing without a valid URL.

$ARGUMENTS may also include an environment type: `local`, `development`, `staging`, or `production`. If provided, pass this context to the skill so findings can be evaluated appropriately. If not provided, infer the environment from the URL when possible (e.g., `.test`/`.local` domains suggest local, `staging.*` subdomains suggest staging). Default to `production` if unclear.

Navigate to $ARGUMENTS and conduct a functional and design-focused QA test.

Follow the testing instructions in skills/functional-design/SKILL.md.

---
title: "Bash Ninja | Create Script as String"
date: 2018-12-04T17:33:38+01:00
draft: false
---

There comes a time I need to write a long `curl` command, interpolated with some variable. And I want to see the whole output of that command, only then I will start to execute it. This is an example of how I do it. And follow by the explanation (mostly for myself) why it work.

### Example
So we Specific example:

{{< highlight bash >}}

script="$(cat <<'EOF'
  API_BASE_PATH="https://swapi.co/api/"
  API_ENDPOINT="starships"

  for starship in `seq 1 2`;
  do
    printf "Starship ${starship}\n"
    curl -X GET "${API_BASE_PATH}${API_ENDPOINT}/${starship}/"
    printf "\n"
  done 
EOF
)"

echo "${script}"
eval "${script}"
{{< /highlight >}}


{{< highlight bash >}}
{{< /highlight >}}

### Why does it work that way?

You can use this boilerplate and change the middle part according to your need.

{{< highlight bash >}}
script="$(cat <<EOF
  do something
  do some other thing
EOF
)"
eval "${script}"
{{< /highlight >}}

`<<EOF` is a [Bash heredoc](https://linuxhint.com/bash-heredoc-tutorial/). And everything inside will be outputted. `cat` command concatenate and print files, in this case, `cat` show the output of heredoc. 

{{< highlight bash >}}
name="Blue Ant"
cat <<EOF
  echo Hello ${name}
EOF

# echo Hello Blue Ant
{{< /highlight >}}

`$(...)` is a form of [Command Substitution](https://www.tldp.org/LDP/abs/html/commandsub.html). It _literally plugs the command output into another context._ In our context, the output of `cat` with heredoc will be assigned to the `script` variable.
 
{{< highlight bash >}}
name="Blue Ant"
script="$(cat <<EOF
  echo Hello ${name}
EOF
)"
eval ${script}

# Hello Blue Ant 
{{< /highlight >}}

Note that without a variable before the command substitution, it doesn't work.
 
{{< highlight bash >}}
name="Blue Ant"
"$(cat <<EOF
  echo Hello ${name}
EOF
)"

# -bash:   echo Hello Blue Ant: command not found
{{< /highlight >}}

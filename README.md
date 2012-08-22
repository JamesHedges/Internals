Internals
=========

This project is all about internals. You know, those things you find yourself cutting and pasting between project, yet never quite keeping each version updated. Sure, it's great to be able to pull code from someplace that solves a problem, and once it works, really, there is no reason to update it unless something new is needed or a bug is found.

Ah yes, but a bug will be found. And you'll fix it in one project, but neglect to fix it in another. And that can be painful.

So what do you do? You create a KitchenSink project. You now have a cool assembly that is separate and contains all of your common bits of code. Now you have two problems. Bugs and keeping all your projects on the latest depedencies. The solution? Well, let's use ilmerge and make it all one assembly. Now you that THREE problems.

Let's recap. That previous paragraph is a world of pain and misery.

Solution?
---------

Create a GitHub repository, call it Internals, and put all your common code in there. Now, put it all in a non-specific namespace like, well, _Internals_.

Now you can add this repository as a submodule to your other projects. The code is in one place, it's all internal (nothing in the Internals repository is marked public, _nothing!_). And the world is a happier place.

How do I use it?
----------------

I thought you would never ask. First, you need to add the submodule to your project. Since we built everything at the root of the Internals project, well, this makes it easy. Just type the following command in your project folder:

```
  git submodule add https://github.com/phatboyg/Internals.git src/YourProjectFolder/Internals
```

This will add a directory to the YourProjectFolder called Internals and pull the _Internals_ repository into that folder.

To see the files in your project, it seems that you can easily add wildcards to a Visual Studio C# Project (.csproj) if you know what you're doing. Because it's never easy with Visual Studio. So open your project file in your favorite text editor (you didn't think you could do this from the IDE did you?).

Locate the section where all of your other item groups are located, and cram the following chunk of code into it:

```
  <ItemGroup>
    <Compile Include="Internals\**\*.cs" />
  </ItemGroup>
```

Once you save, you'll be prompted to reload the project in Visual Studio (do a Save All before you start hacking .csproj files, or you will lose changes).

What about updates?
-------------------

If you want to fetch the latest changes to the Internals project, just go into the Internals folder (so that Git will recognize that you want to operate on the submodule) and type:

```
  git pull
```

If you're lazy like me, you can also take a shortcut:

```
  git submodule foreach git pull
```

This second command will pull the latest for all of your submodules, so if you have more than one make sure that is what you wanted.

Is that it?
-----------

Yes, that's it. Feel free to reference it in your project, feel free to clone and submit pull requests.

Enjoy!

Chris Patterson
@phatboyg

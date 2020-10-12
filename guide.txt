Welcome to my short guide to add new nicknames to the framework.

Needed files:
	your_amazing_mod
		common
			nicknames
				your_amazing_mod_nicknames.txt
			on_action
				your_amazing_mod_on_action.txt
		events
			your_amazing_mod_events.txt
		localization
			your_amazing_mod_l_english.yml
			(your_amazing_mod_l_french.yml, etc.)

In CK2, the nicknames file were where the magic happened.
In CK3, it's merely a place to declare that the nickname exists.
Your nicknames file should look like this:

nick_my_amazing_nickname = {
	is_bad = yes/no		#Whether it's bad or good, default to no
	is_prefix = yes/no	#Whether it's a prefix, default to no
}
nick_my_wonderful_nickname = {} # You can leave out unnecessary statements
...

The on_action file should be fairly simple too.
It just ties the events which will give your nicknames to the random selection.

nickname_selection = { # You must use this name
    random_events = {
		100 = my_amazing_namespace.0001
		100 = my_amazing_namespace.0002
		...
	}
}

Then comes the event file.
First you declare a new namespace for your events.
After that, you list the events which will give your nicknames when chosen by the random selection.

namespace = my_amazing_namespace

my_amazing_namespace.0001 = {
	hidden = yes
	trigger = { # Conditions to get the nickname.
		age >= 20
		has_trait = diligent
		has_trait = ambitious
	}
	weight_multiplier = { # Weight to get the nickname. The higher the value, the more likely a character will get it.
		base = 1
		modifier = {
			factor = 2
			has_trait = calm
		}
	}

    immediate = {
		set_nickname_effect = { NICKNAME = nick_my_amazing_nickname }
    }
}
my_amazing_namespace.0002 = { ... }
...

Lastly, the localization files.
They are just the English, French, etc. text displayed for the nickname.

l_english/l_french/...:
 nick_my_amazing_nickname:0 "the Amazing"
 nick_my_wonderful_nickname:0 "the Wonderful"

And that's it!
Run you mod and enjoy!
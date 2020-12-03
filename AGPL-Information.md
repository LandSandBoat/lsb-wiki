# Applicability
This informative document applies to works we have licensed under the AGPL -- potentially including works which have been submitted to us. As part of the [Limited Contributor License Agreement](https://github.com/project-topaz/topaz/blob/release/CONTRIBUTOR_AGREEMENT.md) which all contributors have agreed to, Project Topaz has permission to license such contributions under the AGPL, and also has permission to apply certain additional terms to the submitted material.

While Project Topaz was forked from [Darkstar Project -- which was licensed under the GPL](https://github.com/DarkstarProject/darkstar/blob/master/LICENSE) -- we have the capability to license and combine new, individual portions of work under the AGPL. For more information on this subject, please see this email exchange with the Free Software Foundation:

<https://raw.githubusercontent.com/wiki/project-topaz/topaz/resources/license/fsf_email.txt>

<https://raw.githubusercontent.com/wiki/project-topaz/topaz/resources/license/fsf_reply.txt>

For the past year, our license document has stipulated the terms under which any of our AGPL works may be used. As we had not yet previously combined AGPL works into the existing software, these terms have not been applicable. Now that Project Topaz has begun integrating AGPL works, it is imperative you understand the terms by which you may use and modify the software.

# Must offer source code to connecting users
[Section 13 of the GPL](https://github.com/project-topaz/topaz/blob/release/GPL3#L552-L561) stipulates that when a work licensed under the GPL has been combined with a work under the AGPL, then Section 13 of the AGPL applies to the combination.

This clause is part of the GPL under which our parent project, Darkstar Project, was licensed. It applies to all servers and codebases derived from Darkstar Project. If you use or modify either Darkstar Project or Project Topaz, then Section 13 of the AGPL applies should your server include an AGPL work. This is true even if you are the author of the modification -- by combining it with an AGPL work, Section 13 of the AGPL applies to your modification.

[Section 13 of the AGPL](https://github.com/project-topaz/topaz/blob/release/AGPL3#L540-L559) states that if you modify the program, and a user interacts with it remotely through a computer network -- if a player connects to your server -- you must offer them access to the source code used in your program. The source code you offer must include any works covered by the GPL. As Section 13 of the GPL stipulates the AGPL’s Section 13 applies to the combination, this includes any modifications to GPL works which are part of the combined program.

These terms are part of the GPL, and have always applied to derivatives of Darkstar Project. Project Topaz need not relicense any GPL works to make this requirement apply. The requirement to offer source code to connected users is automatic when GPL works are combined with AGPL works.

You are not required to contribute your modifications to Project Topaz or any other project. You are only required to provide to connected users a link where your server's source code may be obtained. This source code must be your modified version -- not the original source you received from us. You must make this offer to connected users when they interact with the software. This is upon their first interaction with the software -- not when you feel "ready" to provide it upon a later date.


# Additional terms
Project Topaz's new modifications are licensed under the AGPL. Any person who uses or modifies our works must do so under its terms. Regardless of how permissible usage of Project Topaz may be explained or notated, [the terms of the AGPL](https://github.com/project-topaz/topaz/blob/release/AGPL3) are what govern your usage of our works.

Under [Section 7 of the AGPL](https://github.com/project-topaz/topaz/blob/release/AGPL3#L331-L351), we are permitted to add supplementary "additional permissions" and limited categories of "additional requirements". These supplementary terms -- and their exact text -- may be found in the license file included with the program.

# Additional permissions - "non-retail" modifications exempt
We have added an additional permission to our material exempting you from providing to connecting users any modifications you have made to the software which are "non-retail" customizations and are not for the purpose of stability, security or performance. Our works remain licensed under the AGPL, but provided you have not made "retail" modifications to any portion of the program, you may combine our works with GPL works without triggering Section 13 of our AGPL-licensed works -- they may be used in a program as if they were GPL.

This exemption is revoked if you make "retail" modifications to any portion of the combined work, if you make modifications relating to stability, security, or performance, or if you combine this software with other third-party AGPL works -- works we do not provide ourselves, and thus lack this additional permission we have added to our own works.

A "retail" modification is any modification you make to the combined program which gives the impression of being a recreation of a function or feature from Final Fantasy XI's current "retail servers" -- story, battle content, gameplay, or otherwise. The modification need not be precisely accurate to qualify as a "retail" modification. If a typical connecting user who has experienced content on current "retail servers" and your server can not readily discern differences between the two versions, then it is a "retail" modification which must be offered to connecting users.

Whether modifications are “retail” or “non-retail” is evaluated on an individual basis for each discernible modification. A combination of “retail” behavior with a “non-retail” element does not render the combination “non-retail”. Source code which gives the appearance of emulating any behavior of current “retail servers” are “retail” modifications, and all such modifications must be offered to connecting users.

Modifications made to the combined program for the primary purpose of stability, security, or performance are not included in the exemption our additional permissions grant you -- even should these modifications be very unlike how "retail servers" operate. If you make such modifications to any portion of the combined work, our additional permissions are voided, and you must offer the source code for your modifications to any connecting users.

# Additional requirements - attribution required, misrepresentation forbidden
You are required to retain any author attributions. This includes all copyright notices, information pages or commands, individual author attributions, or lists of contributors in any form. As we have distributed the work as a git repository -- which tracks contributions while including author attribution -- this also includes retaining git author attributions should you redistribute the work to others.

You are forbidden from misrepresenting the origin of our works. You may not claim you are the author of our material or those provided by a contributor to us.

You must differentiate from our program any modified versions which you distribute. You may not advertise or present your version as "Project Topaz" or use our branding -- this includes our names, icons, or example materials which may imply a connection with us.

# Your options
We have made it easier for connecting users to be offered access to your server's source code. As part of a new configuration file, you may insert the URL where you have uploaded your server's git repository. This URL is shown to users upon creation of a new character, and also shown to connecting users upon request when they use new commands we have added.

As the source code offered to connecting users must be that of the server to which they have connected, to ensure that server administrators are fully aware of these license requirements, the software will not allow external connections unless the sample URL in this configuration file has been changed by the server operator. You are free to use the software for your own private use without further action. Should you desire outside users to connect to your server, you will need to provide the configuration file with the URL where connecting users may acquire your source code.

If you do not wish to offer your server's source code to connecting users, then you must replace any required functionality of all AGPL works with your own works. If you are unable -- or unwilling -- to create such works and still wish to withhold your server's source code from connecting users, then your only option is to not use software which contains AGPL works. As Project Topaz now progressively builds AGPL works into its core architecture, this means you should not use Project Topaz if you do not intend to abide by the terms of the AGPL.
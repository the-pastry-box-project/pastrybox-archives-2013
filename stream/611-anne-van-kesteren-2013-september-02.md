

When writing specifications, it is important to describe the world. The model. If you want to write a
specification for zip archives, you would start out explaining the world of zip archives. E.g. “A zip
archive is a map of zip path/zip resource pairs. Zip paths and zip resources are byte sequences.”

On top of this small world you can build other things. For instance, an API. Now if your API supports
enumeration, you run into a problem. You either have to order at the API-level, leave it undefined (bad), or
change the model. You also realize it is not clear whether you can have zero pairs. So you change it: “A zip
archive is an ordered map of zero or more zip path/zip resource pairs.”

You’ll also need to define the mapping of the zip format to zip archive. That is, how you go from the input
byte stream to your model. And maybe the reverse if you support serialization. And slowly your world starts
growing up while staying relatively coherent and clear.

This all may sound relatively trivial, but many specifications fail or struggle to define their world and how
APIs, formats, and URLs interact with it. So I thought I’d mention it and maybe help someone.
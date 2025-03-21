# Google Translate causing "Text content does not match server-rendered HTML"

> Issue #28554 - Created on 3/14/2024

> Original URL: https://github.com/facebook/react/issues/28554

## Description

I know there is a well known bug with google translate, where if you have a conditional text node in a parent with other children, it causes a removeChild error. I suspect this is yet another Google Translate issue, but I can't find any posts about it so i wanted to report it.

This is a snippet from my Next.js 14 project, React 18.2.
```

<div className="md:col-span-4 lg:col-span-5">
                            <div className="mb-2">
                                <Link href="/" className="block">
                                    <span className="flex text-xl font-light">
                                        <Image className="" src={Logo1x} height={64} width={64} alt="Hero" priority placeholder="blur"/>
                                        <div className="flex flex-col justify-center ml-5">
                                            <div className="flex text-xl font-light">
                                                <p className="font-poppins text-white">My Text</p>
                                                <p className="font-poppins text-vai-highlight">My Text2</p>
                                            </div>
                                            <div className="text-sm text-gray-400  transition duration-150 ease-in-out">More text here.</div>
                                        </div>
                                    </span>
                                </Link>
                            </div>
                        </div>
```

The error when using Google Translate to Italian:
```
app-index.js:35 Warning: Prop `alt` did not match. Server: "Eroe" Client: "Hero"
app-index.js:35 Warning: An error occurred during hydration. The server HTML was replaced with client content in <#document>.
Uncaught Error: Text content does not match server-rendered HTML.
```

The interesting part is that if i remove this snippet, i'll see the error pop up on another element - for example, if i remove the <Image> here, then it'll say the first inner-most <p> with 'My Text' changed.

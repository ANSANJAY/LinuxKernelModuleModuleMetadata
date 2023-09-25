### Understanding `MODULE_INFO`

The `MODULE_INFO` macro is used in Linux kernel modules to associate additional metadata with the module. This metadata can be a key-value pair, which provides more information about the kernel module.

```c
MODULE_INFO(tag, value);
```

Here, `tag` is a string literal that represents the type of information being stored, and `value` is the associated value. In your provided code snippet, `MODULE_INFO` is used to associate "name" with "Embedded" and "OS" with "Linux".

### Why is it used?

`MODULE_INFO` is used for the following reasons:

1. **Documentation**: It acts as a form of documentation, providing more context and information about the module.
2. **Debugging**: It can be helpful for debugging by letting developers know more about the running module.
3. **Introspection**: External tools or other modules can use this information to gain insight into the properties or capabilities of a module.

### How to Print Module Tags?

In your example, the module name and version are printed using the `THIS_MODULE` macro which points to the current module structure (`struct module`). However, the `MODULE_INFO` tags like "name" and "OS" that you have set are not directly accessible via `THIS_MODULE` macro or any direct module structure. Typically, such information might be extracted via user-space tools.

If you need to access these values within the kernel module, you might have to manually define them as constants or variables and then print or use them as needed.

For example:

```c
#define MY_MODULE_NAME "Embedded"
#define MY_MODULE_OS "Linux"

MODULE_INFO(name, MY_MODULE_NAME);
MODULE_INFO(OS, MY_MODULE_OS);

static int __init mod_init(void)
{
	pr_info("name = %s\n", MY_MODULE_NAME);
	pr_info("OS = %s\n", MY_MODULE_OS);
	return 0;
}
```

In this manner, you can access and print the module tags as you have defined using `MODULE_INFO` by using variables or constants.
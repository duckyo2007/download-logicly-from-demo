# Download-.logicly-on-logic.ly-demo-for-free
Download .logicly on logic.ly/demo for free

just paste this code to the console of devtools:
"
(() => {
    const findStore = (el) => {
        const key = Object.keys(el).find(k => k.startsWith('__reactFiber$') || k.startsWith('__reactInternalInstance$'));
        let fiber = el[key];
        while (fiber) {
            if (fiber.stateNode && fiber.stateNode._store) return fiber.stateNode._store;
            if (fiber.memoizedProps && fiber.memoizedProps.store) return fiber.memoizedProps.store;
            fiber = fiber.return;
        }
        return null;
    };
    const targetEl = document.querySelector('.primary-editor') || document.body.firstElementChild;
    const store = findStore(targetEl);
    if (!store) {
        alert("Not found!);
        return;
    }
    const action = { type: "saveDocument", deflate: true };
    store.dispatch(action);
    const fileName = (store.getState().file?.name || "Untitled Circuit") + ".logicly";
    const blob = new Blob([action.data], { type: "application/octet-stream" });
    const url = URL.createObjectURL(blob);
    const a = document.createElement("a");
    a.href = url;
    a.download = fileName;
    document.body.appendChild(a);
    a.click();
    a.remove();
    URL.revokeObjectURL(url);
})();
"

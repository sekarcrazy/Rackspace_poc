first commit

trying to access SSH..

>>window.navigator.userAgent
"Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 6.1; WOW64; Trident/4.0; SLCC2; .NET CLR 2.0.50727; .NET CLR 3.5.30729; .NET CLR 3.0.30729; .NET4.0C; .NET4.0E)"



6542ca1f559a3aa63cea938f6d407adc840faa744c231106baa86a0fd5813185dd4bb55c9e97c73b146d35a3b61118d573e2caa1260190b0dd6456ec32785c65e0f53b642c895c0ca256be03d9602b3b6ccade4a354123bdcea156acbd06ef90b738519a8a35bf58ff6d777dbae75770bda73811aea96cecb92e63204f57ad88611fb147eedf60e100edac1eae6868569c0a3458739804847ebd6500b21d576f66a025c2fa3c0967dc6c00ce2fd032374884d7c5af9504941fed59f8483767ffef5e250ebb4324cdd279bae98ded5c6dd2776d6ba526f2a7cf2ab0286fc7c2237f16691c8dc18e46c376884a527e77348daea64dae324f53c44f4da9e97ec4d4



async function importModuleFromDealTracker(resolveBy = null, defaultResolveBy = null, params) {
    if(!defaultResolveBy){
        throw new Error("defaultResolveBy cannot be empty...");
    }
    var module = null;
    var formattedPath = resolveBy || defaultResolveBy;
    formattedPath =  setUrlParams(formattedPath, params);
    var moduleLoader = {
        loader: async (path) => import(`../../DealTracker/${path}` /* webpackMode: "eager" */ ), // Need to pass full path to resolve by webpack
    }
    try{
        module = await moduleLoader.loader(formattedPath);
        return module;
    }catch(e){
        module = await moduleLoader.loader(defaultResolveBy);
        return module;
    }
}

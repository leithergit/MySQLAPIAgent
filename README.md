# MySQLAPIAgent
为MySQL数据库 API提高性能C++封装！
Sample Code:
try
	{	
		// 使用数据信息构造连接对象指针
		CMySQLAgent* pMySQLAgent = new CMySQLAgent(m_strServerIP,m_strDBAccount,m_strDBPassword,m_strDBName,m_nDBPort);
		
		// 支持类似printf函数格式不定参数输入，并将结果返回到结果集对象Result中
		CMyResult Result = pMySQLAgent->Query("select orgname,coding from organization order by coding where deviceid = %s",m_strDevID);
		
		int nIndex = 0;
		do 
		{
			// 支持以列名直接获取数据结，并根据变量类型自动返回相应数据
			string strOgrname = Result["orgname"];
			string strCoding = Result["coding"];
			
		} while (++Result);	// 目前结果集CMyResult类仅支持前置自增操作，即类型++Result
		
		// CMyResult对象可以直接赋值新的结值，原结果集将被释放
		Result = pMySQLAgent->Query("SELECT max(`deviceid`) AS maxDevid FROM devices;");
		
		string strMaxID = Result["maxDevid"];
		
	}
	catch (CMySQLException& e)
	{// 当连接数据异常，访问字段名不存在时，将会抛出异常，e.what_返回具体异常描述信息
		string strException = e.what_;
	}
	catch(std::exception &e)
	{
		const char *szError = e.what();
	}
